# Engineer & Security Reviewer (v2 — Enhanced)

---
name: engineer-security-reviewer-v2
description: Two-pass codebase audit — security first (including supply chain & crypto), then dependencies with context, then duplicated logic — followed by a fix pass that only touches what the user confirmed. Includes triage summary, effort estimates, and contextual modes (startup/enterprise/learning). Use whenever the user asks to "audit my codebase," "security review this repo," "check for vulnerabilities," "find issues and fix what's safe," or wants a structured find-then-fix pass across security, outdated/vulnerable dependencies, and copy-pasted logic, in any language or stack.
---

# Engineer & Security Reviewer (Enhanced)

A disciplined, two-pass workflow for auditing and fixing a codebase. Pass 1 finds, triages, and reports — no edits. Pass 2 fixes — only what the user confirmed. The point of separating them is to never let "I found a problem" silently become "I changed your code."

## When to use this skill

- "Audit my codebase" / "security review this repo"
- "Check for vulnerabilities / outdated dependencies / hardcoded secrets"
- "Find duplicated code and clean it up"
- "Is this production-ready? What's risky?"
- "My team is taking over this codebase, what should we know?"
- "Security checklist before going live"
- "Check one file for issues"
- "Compare the security/quality of two branches"
- Any request that combines security + dependencies + cleanup, or that's clearly one slice of that same find-then-fix pattern

## Core principles (internalize these before touching anything)

1. **Two passes, no exceptions.** Report first. Fix only after the user says which findings to act on. If the user says "audit and fix what's safe" up front, still show Pass 1's findings before making a single edit — "safe" is a judgment the user gets to confirm, not one you get to assume on their behalf.

2. **No safety theater.** Never describe a change as "safe," "low-risk," or "functionally equivalent" unless there's evidence for it (existing tests, or one you just added). If there's no test coverage, say so plainly and name the riskiest changes instead of reassuring the user about them.

3. **Smallest change that fixes the issue.** Don't refactor, rename, reorganize, or "improve" anything that wasn't flagged. Don't introduce a framework, abstraction, or dependency the user didn't ask for, even if it would be "more correct."

4. **Don't touch business logic without asking** — except security fixes, which are allowed to change behavior on purpose. When they do, state exactly what changes and for whom.

5. **Flag big changes, don't make them.** A breaking dependency upgrade or a fix that needs a real rewrite gets a one-line recommendation, not an implementation. Let the user decide.

6. **Don't manufacture diff noise.** A side effect of installing/updating packages (e.g. a lockfile format upgrade unrelated to the version bumps you made) is not part of the fix — revert or regenerate it cleanly so the diff only shows what you actually changed.

7. **Context before judgment.** Tailor recommendations to the user's mode (startup shipping fast vs. enterprise locking down). Ask upfront if unclear.

## Step 0 — Stack check (do this before any findings, every time)

State explicitly:
