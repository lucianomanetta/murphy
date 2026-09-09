# Privacy

Murphy is local-first. Its observation and reporting flow stores evidence locally; it does not require a Murphy cloud service or upload task context as part of monitoring.

Endpoint observation records metadata such as file paths, processes and connection addresses. It is not a general file-content recorder. Optional task-context integration can retain the original task prompt and workspace locally, so that information may itself be sensitive. It does not record complete conversations as a general feature.

Local retention is bounded. Routine detail expires; summaries and relevant evidence have finite capacity. Exported reports are separate files and require your own storage and sharing decisions.

Treat local data and reports as sensitive. Review and sanitize reports before sharing. A report can contain paths, task information and technical identifiers even though monitoring does not read file contents.

Agents may independently contact their model providers. Their network use and privacy policies are separate from Murphy's local monitoring.

This public repository contains documentation and synthetic demonstration images, not user evidence or task prompts from real sessions.
