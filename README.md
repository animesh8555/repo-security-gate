# Repository Security Gate

Review a repository before giving it access to your machine, credentials, or network.

Repository Security Gate is a reusable set of instructions for coding agents. It asks the agent to pause an installation, inspect the code and dependencies, fix supported findings, and verify the result before continuing.

**This is a review workflow, not a security sandbox or an installation interceptor.** It does not run a scanner by itself, monitor your computer, or guarantee that a repository is safe.

## Use it with your agent

Read [SKILL.md](SKILL.md) before adopting it. It is the canonical workflow and has no runtime dependencies.

For an agent that supports `SKILL.md` skills, place this folder in the agent's documented skill location. The optional `agents/openai.yaml` supplies Codex display metadata; other agents can ignore it.

For any agent that can read Markdown instructions, attach `SKILL.md` or ask it:

> Read SKILL.md from my local repo-security-gate checkout. Apply it to TARGET_REPOSITORY. Review and fix supported findings before running the requested installer. Keep the installation blocked or pending if required checks cannot be completed safely.

Replace TARGET_REPOSITORY with the actual path or URL. Give the agent access only to the files and tools needed for that review.

In Codex, after installing the folder as a skill:

```text
Use $repo-security-gate before installing this repository: TARGET_REPOSITORY
```

For existing installations:

```text
Use $repo-security-gate to audit repositories under PROJECTS_DIRECTORY.
Report each repository separately. Do not reinstall anything.
```

To make review a standing instruction, add a reference to your agent's supported user or project instructions:

> Before installing, updating, enabling, building, or running third-party repository code, read my local repo-security-gate/SKILL.md and follow its gate. Do not continue when the outcome is BLOCKED or PENDING.

Resolve that reference to your actual local path. Instruction discovery differs by agent; verify that yours loads it. There is no universal automatic-install hook in this project.

## Get it on Agensi

[Use Repository Security Gate for free on Agensi](https://www.agensi.io/skills/repository-security-gate).

The same workflow is available here under the [MIT license](LICENSE).

## What it checks

- API keys and other secrets in code, history, logs, and browser bundles.
- Sensitive-file reads and data sent to third-party endpoints.
- Install hooks, downloaded payloads, persistence, plugins, and MCP commands.
- Dependency advisories and supply-chain risks.
- Relevant access-control, injection, path-handling, and server-side request issues.

The agent must trace behavior rather than treat every network request as malicious. It must not test with real secrets or upload private source to an external scanner.

## Review outcomes

| Outcome | Meaning |
| --- | --- |
| BLOCKED | An unresolved security issue or unsafe install path was found. |
| PENDING | Required evidence, checks, isolation, or authorization is missing. |
| CLEARED FOR REVIEWED INSTALL | The reviewed version passed the required checks; the already authorized install may continue. |

Clearance applies to the reviewed source, dependencies, configuration, and command. A change can require another review. Exposed credentials still need rotation even after a code fix.

## Compatibility and limits

The workflow is plain Markdown and can be supplied to any agent that accepts instructions. Native installation, automatic discovery, tool access, and sandbox enforcement depend on the host. Cross-agent behavior has not been certified. A chat-only assistant can discuss findings but cannot inspect local files or enforce an installation pause without tools.

There are no bundled scanners, executable installers, background services, telemetry, or network clients. An agent may use trusted external tools during a review; their coverage and data handling need separate consideration.

## Suggestions and contributions

Suggestions, bug reports, and pull requests are welcome. See [CONTRIBUTING.md](CONTRIBUTING.md) and the issue templates. For vulnerabilities in this project, follow [SECURITY.md](SECURITY.md). For the small set of manual behavior checks, see [tests/scenarios.md](tests/scenarios.md).

Licensed under [MIT](LICENSE).
