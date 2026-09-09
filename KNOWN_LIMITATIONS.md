# Known limitations

- Windows x64 is the current target. This publication does not claim ARM64 or clean-machine certification.
- Standard observation is sampled and may miss short-lived activity. It does not provide file read/delete telemetry.
- Deep Audit observes supported file requests, not guaranteed successful operations. Overload, unavailable evidence and shutdown boundaries can leave gaps.
- Product recognition is not authenticated application identity or conversation ownership. Shared hosts and generic descendants may remain ambiguous.
- Workspace context is optional. Received context does not mean an action was authorized by a person; missing context remains unknown.
- Background presence does not prove inactivity, and process presence alone does not mean an agent is actively working.
- Network observations do not establish transmitted contents, exfiltration or universal hostname attribution. DNS and UDP coverage are not claimed.
- Rename visibility can be incomplete; seeing names does not prove a successfully completed paired rename.
- Local retention and report detail windows are bounded. Expired details cannot be reconstructed from a summary.
- The live Markdown report covers a recent retained window, up to 2,000 records / 16 MiB, with current findings. It states its cutoff and covered interval; it is not a complete lifetime archive or necessarily the same as the on-screen filters.
- Technical integrity information is not absolute forensic proof, proof of complete capture or protection against a fully compromised endpoint.
- Windows controls notification delivery; a suppressed notification does not mean no finding exists. Check the application.

No attack prevention, universal threat detection, intent authentication or complete machine visibility is promised.
