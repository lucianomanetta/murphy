# An agent's report is not evidence

**What I learned building independent observability for AI coding agents**

Luciano Manetta

---

A coding agent finishes a task and tells you what it did. It lists the files it changed, the tests it ran, the problem it solved. The report is coherent, well structured, and often correct.

It is also the only account you have, written by the party being assessed.

I spent a long time treating that report as the record of what happened. Then I started shipping systems into Brazilian tax and labour compliance, where a wrong output has a legal consequence and someone eventually has to defend every number in front of an auditor. In that setting the question changed shape. The question stopped being "did the agent say it worked" and became "can I show what the agent actually touched".

Those are different questions, and the gap between them is the subject of this piece.

## Why self-report fails, and how it fails

The failure mode people expect is a lying agent. That is not what I found, and framing it that way makes the problem harder to see.

What I found is narrower and more interesting. An agent's report is a summary written from its own context window, and that context is a lossy, partial view of a system with far more state than the agent can hold. The report is usually accurate about intent. It is less reliable about effect.

Concretely, the recurring gaps were these.

**Work attributed to the wrong cause.** A test passes. The agent reports the fix worked. The test was passing before the change for an unrelated reason, and the agent had no way to know that because it never observed the prior state independently.

**Side effects outside the narrative.** The agent describes editing three files. Four were written. The fourth was a cache, a lockfile, a generated artifact, or a config the tooling rewrote as a consequence of something the agent ran. None of this is deception. It simply falls outside what the agent considered worth reporting.

**Completion claimed at the boundary of knowledge.** The agent finishes the part it can see and reports the task complete, because from inside its context the task *is* complete. The remaining work lives in a part of the system it was never shown.

**Silent scope drift across long tasks.** Over a long session the agent's working understanding of the goal moves. Each individual step is defensible. The sum of the steps is not what was asked. The final report describes the drifted goal, coherently, because that is the goal the agent now holds.

None of these require bad faith. They are the ordinary consequence of asking a system with partial observability to report on its own effects.

## What independent observation means

The fix is not a better prompt asking the agent to be more careful. Asking the subject to assess itself more rigorously produces a more confident subject.

The fix is to reconstruct what happened from outside the agent, using signals the agent does not author.

I built a tool for this. It watches the machine and not the conversation: process ancestry, so I can see what was actually launched and by what; filesystem activity, so I can see every path written and not only the ones mentioned; workspace boundaries, so I can see when something reached outside the directory it was supposed to stay in; and network behaviour, so I can see what was fetched.

Then it compares that reconstruction against the agent's own account.

The comparison is the product. Either signal alone is weak. The machine record tells you what happened and nothing about why. The agent's report tells you the intent and may be incomplete about the effect. Held against each other, the places where they disagree are exactly the places worth a human's attention.

## The taxonomy that made it usable

The first version of this was close to useless, and the reason is worth stating. It produced a flat list of everything observed, which is an enormous amount of noise, and left a human to work out which items mattered.

What made it usable was separating four things that had been collapsed together.

**Observed fact.** This path was written at this time by this process. No interpretation.

**Inference.** This write was probably caused by that command. Defensible, derived, and labelled as derived.

**Uncertainty.** Something happened here that the evidence does not resolve. Naming this explicitly turned out to matter more than I expected, because the alternative is silently guessing and presenting the guess at the same confidence as a fact.

**Claimed completion.** What the agent said. Kept separate, never promoted to fact by proximity to one.

Once those four were distinct, the output became reviewable. A person can scan a list of disagreements between claim and observation in a minute. Nobody reviews a flat log of 50,000 events.

## What showed up at scale

I validated the evidence model from small controlled scenarios up to more than 50,000 observed operations.

The headline finding is not that agents misbehave. At scale, the overwhelming majority of what an agent does is exactly what it says it does.

The finding is about where the exceptions cluster. They are not uniformly distributed. They concentrate in long-running tasks, in tasks that cross a subsystem boundary, and in tasks where the agent had to make an unprompted decision about scope. Those three conditions predict almost all of the divergence I saw.

That is operationally useful, because it tells you where to spend review attention. A short, well-bounded change inside one module rarely needs independent verification. A four-hour task that touched the auth layer and the data model and decided on its own to refactor something adjacent is where the review budget belongs.

## The productivity finding I did not expect

The thing I set out to catch was the agent doing more than it said.

The thing that cost me the most time turned out to be the opposite: the agent doing far more than the task required, and being unable to tell that this was a cost.

Watching sessions at the process level made this impossible to miss. A narrow change to one function would trigger a full regression suite. Components that had been validated, shipped, and running in production for months would be re-proven from scratch on every pass. Gates nobody asked for would be invented and then satisfied. Thirty minutes of machine time and a great deal of my attention would go into establishing something that was not in question.

This reads as rigour. Measured, it is mostly cost.

The correction I settled on is proportionality, made explicit in the instructions and never left to the agent's judgement:

- Focused validation by default, scoped to what the change can actually reach.
- Broad regression where a change is structural, crosses a boundary, or has a real blast radius.
- Components already homologated are not re-proven on every change. They are re-proven when something they depend on moves.
- Operational blockers and code blockers are separated. An agent stuck on a missing credential should say so and stop, not start redesigning.

Caution that is not proportional to risk is not safety. It is overhead wearing safety's clothes, and it is where I see most agent time disappear.

## What this means if you are rolling agents out to a team

Three things I would tell a team adopting coding agents seriously.

**Decide what you need to be able to prove.** In an unregulated codebase, the agent's report plus code review is probably enough. The moment output has to be defended to an auditor, a regulator, or a court, you need a record that does not originate with the thing being audited. Work out which of those you are before you scale.

**Spend review attention where divergence concentrates.** Long tasks, boundary crossings, unprompted scope decisions. Reviewing everything uniformly is the same as reviewing nothing, because attention runs out.

**Write proportionality into the instructions.** An agent will not infer the right amount of caution from first principles, and left alone it will drift toward more. Tell it what a narrow change deserves and what a structural one deserves, and the time you get back is substantial.

---

The general lesson is older than any of this. When a system reports on itself, its report is a claim. Whether the claim needs independent verification depends entirely on what it costs to be wrong. Coding agents have not changed that calculation. They have made it apply to a great deal more of the work.
