# Compatibility and coverage

Public baseline: Murphy 0.1.4.17 for Windows x64. These are conservative capability descriptions, not guarantees for every version, installation or session. Installing an agent or enabling an integration is not proof of full context coverage.

| Agent / surface | Public coverage status | Scope |
| --- | --- | --- |
| Claude Code | FULL_CONTEXT, conditional on evidence for the individual task | The cooperative task-context flow has been validated with a real Claude Code task and independent Windows observations. A particular task may still be partial or unavailable. |
| Claude Desktop | ENDPOINT_ONLY when recognized | Separate from Claude Code when available process evidence supports that distinction. Desktop presence does not imply Code task context. |
| Codex | PARTIAL_CONTEXT | A controlled context workflow has been observed. Do not treat this as universal, automatic FULL_CONTEXT across Codex surfaces. Endpoint visibility remains separately available. |
| Gemini CLI | NOT_VALIDATED for task context | A supported integration option does not establish a validated end-to-end task flow. Recognition alone does not change this status. |
| Antigravity | ENDPOINT_ONLY when recognized | Process and related endpoint observations are available within supported recognition paths. No full task-context claim. |
| Cursor and other recognized candidates | NOT_VALIDATED for end-to-end context | Recognition can provide endpoint observations; no blanket compatibility certification is claimed. |
| Browser tabs and shared application hosts | LIMITED_ATTRIBUTION | Murphy cannot infer a particular AI, conversation or tab solely because a browser or shared host is running. |

FULL_CONTEXT means the supported task context and endpoint evidence can be correlated for that task. It does not authenticate identity, prove human approval, establish intent or guarantee complete capture.

Standard mode uses sampled process/network observations. Deep Audit adds supported file requests with elevation. Missing, ambiguous or expired evidence reduces what can be stated. Consult the coverage displayed for the actual agent and task.
