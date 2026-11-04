# Contributing

Open an issue for a missing check, unclear instruction, or a case where an agent made the wrong decision. Include the host agent, a sanitized reproduction, expected result, and actual result. Never include live credentials, private source, or personal files.

Keep pull requests focused on one problem. Explain why the existing instructions fail and how the change fixes that case. Prefer a short instruction over a new script or dependency. Comments in any future code should explain a non-obvious reason, not repeat the code.

Before submitting:

- Read the diff and check for credentials, personal paths, and unrelated files.
- Check relative Markdown links and skill frontmatter.
- Walk through the applicable cases in tests/scenarios.md; record the agent/version and tools if you actually run them.
- Describe remaining limits. Do not claim universal compatibility or guaranteed detection.

Small documentation fixes do not need a new behavioral test. Changes to the gate should include a scenario demonstrating the intended decision. Use synthetic data and isolated fixtures; never execute a malicious sample on your host.

Be respectful and address the technical issue. Review timing depends on maintainer availability.
