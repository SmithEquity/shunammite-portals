# execution/

Deterministic scripts live here. Rule of thumb: if a step should produce the same output every time given the same input (API calls, formatting, file operations), it belongs in a script here — described by the owner, written by the AI, tested once together.

None yet. First candidates, when a real bottleneck demands them:

- Cross-page consistency checker (prices, links, footer text across all portal HTML files)
- Link validator for the portal ladder
