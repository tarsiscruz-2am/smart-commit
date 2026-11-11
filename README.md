# Smart Commit

**An AI-powered skill for organizing Git changes into logical, dependency-aware commits.**

Smart Commit helps developers create cleaner, more consistent Git histories by analyzing implementation context, repository changes, and project-specific commit conventions.

Instead of combining an entire implementation into a single commit, it proposes cohesive, independently reviewable commit groups, each with an appropriate message and execution order.

Built on the open [Agent Skills](https://agentskills.io) format, Smart Commit is designed to work across compatible AI coding agents.

## Features

- **Context-aware analysis:** Uses the available AI conversation history to understand implementation decisions and dependencies.
- **Intelligent commit grouping:** Organizes changes by logical responsibility rather than simply grouping files by directory or ticket.
- **Dependency-aware sequencing:** Suggests an appropriate commit order based on relationships between changes.
- **Project convention compliance:** Reads `BRANCHING_STRATEGY.md` to follow repository-specific commit rules.
- **Consistent commit messages:** Generates descriptive English commit subjects and structured bullet-point descriptions.
- **Human-in-the-loop workflow:** Presents a complete commit plan and requires explicit approval before creating commits.
- **Safe Git operations:** Stages only approved changes without automatically pushing or modifying existing commits.

## Supported AI Agents

Smart Commit follows the Agent Skills format and can be used with compatible AI coding agents, including:

- OpenAI Codex (CLI, IDE extension, and desktop app)
- Claude Code
- Cursor
- GitHub Copilot
- Other agents supporting the Agent Skills format

Compatibility and available capabilities may vary by agent.

## Installation

Install Smart Commit globally using the Skills CLI:

```bash
npx skills add tarsiscruz-2am/smart-commit -g
```

Select your preferred AI agent when prompted.

Alternatively, install it manually by placing the `smart-commit` directory in your agent's supported skills directory.

For agents supporting the universal directory:

```text
~/.agents/skills/smart-commit/
└── SKILL.md
```

## Requirements

Before using Smart Commit, ensure that:

- Your AI coding agent supports Agent Skills and has access to Git operations.
- You are working inside a Git repository with changes ready to organize.
- The repository contains an accessible `BRANCHING_STRATEGY.md` defining its commit conventions.
- Your agent has access to the relevant implementation context when available.

The skill uses Git as the source of truth for actual changes and the project's branching strategy as the authority for commit conventions.

## Usage

After completing an implementation, invoke the skill in your AI coding agent:

```text
$smart-commit
```

For better results, run it in the same conversation used to implement the ticket, allowing the agent to consider the original requirements, technical decisions, and implementation context.

### Workflow

1. **Analyze:** Reviews implementation context, Git changes, and repository conventions.
2. **Group:** Identifies cohesive changes and determines their dependencies.
3. **Plan:** Proposes an ordered sequence of commits, including files, messages, and grouping rationale.
4. **Review:** Waits for developer approval before modifying Git.
5. **Execute:** Stages the approved changes and creates each commit individually.
6. **Verify:** Reports the created commits and any remaining uncommitted changes.

**Smart Commit never creates commits without explicit approval.**

## Example Output

Suppose an implementation introduces shared document utilities and new contract fallback behavior.

Smart Commit might propose:

### Commit 1 — Shared Utilities

**Files:**

- `src/utils/document-utils.ts`
- `src/services/contract-service.ts`

**Commit message:**

```text
refactor(contracts): extract shared document utilities

- extracted reusable document lookup logic
- simplified contract service dependencies
```

**Reason:** Establishes reusable functionality before introducing behavior that depends on it.

### Commit 2 — Contract Fallback

**Files:**

- `src/hooks/use-contracts.ts`
- `src/components/contract-details.tsx`

**Commit message:**

```text
feat(contracts): add document fallback behavior

- added fallback for missing contract documents
- updated document selection behavior
```

**Reason:** Introduces the feature using the shared functionality established in the previous commit.

### Proposed Execution Order

| Order | Commit                            | Dependency |
| ----- | --------------------------------- | ---------- |
| 1     | Extract shared document utilities | None       |
| 2     | Add document fallback behavior    | Commit 1   |

The developer can review the proposed grouping, request adjustments, or approve execution.

The example is illustrative. Actual grouping depends on the implementation and repository conventions.

## Commit Conventions

Smart Commit follows the repository's `BRANCHING_STRATEGY.md` rather than enforcing a universal commit naming strategy.

Its default message guidelines include:

- English commit subjects and descriptions.
- Descriptive commit types and scopes when required.
- Bullet-point descriptions beginning with lowercase, past-tense verbs.
- A maximum of 100 characters per description bullet.
- Clear separation of independently reviewable changes.

Repository-specific conventions take precedence.

## Safety and Developer Control

Smart Commit is designed to assist developers, not replace their judgment.

By default, it:

- Never stages or commits changes during planning.
- Requires explicit approval before execution.
- Avoids staging unrelated files.
- Preserves existing staged changes unless reorganization is approved.
- Never pushes automatically.
- Never amends existing commits without permission.
- Never discards user changes.

Developers retain control over the final commit structure.

## Contributing

Contributions are welcome!

Smart Commit is intended to evolve through real-world usage across different repositories, workflows, and AI coding agents.

Areas where contributions are especially valuable include improving commit grouping accuracy, dependency analysis, compatibility with different agents, and support for additional project conventions.

If you have an idea, encounter unexpected behavior, or identify an opportunity for improvement, feel free to:

- [Open an issue](https://github.com/tarsiscruz-2am/smart-commit/issues) to report bugs or suggest enhancements.
- Submit a Pull Request with improvements.
- Share examples of commit plans that could be organized more effectively.

The goal is to build a reliable, collaborative tool that makes Git histories easier to understand, review, and maintain.

## Resources

- [GitHub Repository](https://github.com/tarsiscruz-2am/smart-commit)
- [Agent Skills Specification](https://agentskills.io)

---

**Smart Commit — Better commit organization, less manual effort, and full developer control.**
