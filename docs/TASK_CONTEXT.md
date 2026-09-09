# Task context

A supported integration can provide task information such as the prompt, session and workspace. When relevant Windows evidence can be correlated, Murphy can compare activity with the received task context without requiring the same workspace to be entered manually.

Enable an integration deliberately in Settings. For compatible integrations, Murphy may install or remove only the context hooks it needs while preserving unrelated agent settings. A configured integration does not by itself prove coverage; inspect its status for the actual task.

Claude Code and Claude Desktop are different surfaces. Enabling the Claude Code integration does not give Desktop the same task context.

Context received from an integration is cooperative information. It is not human authorization, authenticated intent or proof that an action was permitted. Activity outside a received workspace can be legitimate and needs interpretation.

Unavailable context and incomplete evidence are limitations, not reasons to invent a task relationship. See the [compatibility matrix](../COMPATIBILITY.md).
