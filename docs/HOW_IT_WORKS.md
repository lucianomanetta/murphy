# How Murphy works

Murphy observes supported activity on the same Windows endpoint as the agent. It relates available process, file and network observations, groups routine activity, and presents relevant items for review.

Conceptually:

**Windows observations → local activity record → contextual interpretation → understandable activity and findings**

Optional integration context supplies information about the task, such as its workspace. It helps explain observations when the relationship is supported by evidence. It does not replace the independent observation or grant permission.

The overview answers which recognized agents have live processes. Activity answers what was recently observed. Technical details and reports support closer inspection without filling the main view with implementation terminology.

Routine background maintenance may be grouped. Grouping does not turn an observation into proof of success or hide the distinction between routine activity and pending findings.
