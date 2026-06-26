# Engineer & Security Reviewer

A disciplined, **two-pass codebase audit skill** for finding and fixing security issues, outdated dependencies, and duplicated logic — in any language or stack.

## 🎯 What it does

**Pass 1 — Find & Report** (no edits)
- 🔐 Security checks (hardcoded secrets, injection risks, auth gaps, supply chain threats, crypto issues, CORS, DoS protection)
- 📦 Dependency audit (vulnerabilities, outdated packages, license conflicts)
- 🔄 Duplication detection (copy-pasted logic, maintenance risk)
- 📊 Triage summary (findings count + effort estimates)

**Pass 2 — Fix** (only after confirmation)
- ✅ Apply security fixes (with behavior change explanations)
- 📦 Bump dependencies (patch/minor freely, flag major versions)
- 🧹 Safe cleanups (only approved duplication extractions)
- ✓ Verification post-fix (build, test, linter checks)

---

## 🚀 Quick Start

### Via GitHub (for Claude AI)

1. **Access this repository**: https://github.com/freemind25/engineer-security-reviewer
2. **Copy the `SKILL.md` file** into your Claude conversation
3. **Share your codebase** (files, folder structure, package manifests)
4. **Ask Claude** to audit your repo:
"Audit my codebase for security, outdated deps, and duplication"

perl

### Via npm (coming soon)

```bash
npm install engineer-security-reviewer

Then reference SKILL.md in your prompts.
📋 What Gets Audited
Security (Priority)

    ✅ Hardcoded secrets (API keys, tokens, passwords, DB credentials)
    ✅ Input validation (SQL injection, command injection, XSS, path traversal)
    ✅ Auth/Authorization (missing checks, broken middleware)
    ✅ Sensitive data exposure (logs, localStorage, URLs)
    ✅ Unsafe code execution (eval, unsafe deserialization, dangerous HTML)
    ✅ Cryptography & randomness (weak algorithms, hardcoded keys)
    ✅ CORS & cross-origin risks (wildcard + credentials)
    ✅ Supply chain integrity (post-install scripts, typosquatting)
    ✅ Rate limiting & DoS protection (brute-force, unlimited endpoints)
    ✅ Configuration & defaults (hardcoded vs env vars, HTTPS, cookies)

Dependencies

    ✅ Vulnerability scan (CVE severity, fix availability)
    ✅ Outdated packages (current vs latest versions)
    ✅ License compatibility (GPL, MIT, Apache conflicts)
    ✅ Dev vs Prod misclassification
    ✅ End-of-life / unmaintained packages
    ✅ Pinning inconsistencies

Duplication

    ✅ Copy-pasted logic (validation, API calls, error handling, formatting)
    ✅ Maintenance burden assessment
    ✅ Extraction feasibility (cost vs benefit)

🎯 Core Principles

    Two passes, no exceptions — Report first, fix only after confirmation
    No safety theater — "Safe" only if there's test evidence
    Smallest change — Don't over-engineer or refactor unrelated code
    Business logic stays hands-off — Except security fixes (which can change behavior intentionally)
    Context matters — Adapt to startup (ship fast) vs enterprise (comprehensive) modes
    No diff noise — Only show intentional changes

📖 Full Documentation

See SKILL.md for the complete two-pass audit workflow, including:

    Step 0: Stack detection (language, framework, tests, deployment)
    Pass 1: Detailed findings, triage summary, context mode selection
    Pass 2: Fix workflow, pre-flight checklist, verification post-fix
    Closing summary: Concrete recap of all changes

📊 Example Audit Flow

vbnet
User: "Audit my Node.js API. It's a startup, ship fast."

↓ Step 0
Detect: Node 18 + Express 4 + Jest tests ✅

↓ Pass 1 — Find & Report
3 security issues (2 high, 1 low)
5 outdated deps (1 critical CVE)
2 duplication patterns
Triage: "5 mins critical security, 15 mins for CVE"

↓ User confirms scope
"Fix critical + CVE, skip cleanup"

↓ Pass 2 — Fix
Apply 2 security fixes + 1 dep bump
Tests pass ✅

↓ Closing Summary
✅ 2 security issues fixed
📦 1 dependency updated
🚀 Ready to merge

🏆 What's New in v2

    ✨ Supply chain security checks (post-install scripts, typosquatting)
    ✨ Dependency context table (Risk, Used in, Licenses)
    ✨ Duplication criteria (when to extract, extraction cost)
    ✨ Triage summary (findings count + effort estimates)
    ✨ Context modes (Startup / Enterprise / Learning)
    ✨ Pre-flight checklist (files, behavior changes, risk level)
    ✨ Verification post-fix (build, test, linter checks)
    ✨ Quick commands (narrow scope, compare branches)

📦 Installation
Option 1: Direct from GitHub

bash
# Clone and use locally
git clone https://github.com/freemind25/engineer-security-reviewer.git
cat SKILL.md  # Copy into your prompts

Option 2: npm (coming soon)

bash
npm install engineer-security-reviewer
# Then reference in your prompts

🤝 Contributing

Found a gap in the audit? Want to suggest a new check?

    Open an issue: https://github.com/freemind25/engineer-security-reviewer/issues
    Describe the finding/improvement
    Submit a PR with the suggestion

📜 License

MIT — Use freely, modify as needed, no attribution required.
🚀 Next Steps

    Try it: Share your codebase + ask Claude to audit it
    Provide feedback: What was useful? What's missing?
    Contribute: Suggest improvements or new checks

Questions? Open an issue or start a discussion!

Made with ❤️ for codebase audits done right.

markdown

**Commit message:**

docs: add comprehensive README with setup and examples

yaml

---

## Fichier 3 : `CHANGELOG.md`

**Add file** → **Create new file**

Nommez-le : `CHANGELOG.md`

Collez ceci :

```markdown
# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [2.0.0] — 2024-01-XX

### ✨ Added

#### Security Enhancements
- **Supply chain security checks**: Post-install scripts, suspicious package names (typosquatting), unsigned commits, package provenance
- **Extended crypto checks**: Deprecated algorithms (MD5, SHA1), hardcoded keys, weak cipher modes
- **Rate limiting audit**: Brute-force protection on login, API endpoint limits, abuse prevention
- **Configuration audit**: Hardcoded DB credentials vs env vars, default passwords, debug mode, HTTPS enforcement, cookie flags

#### Dependency Management
- **Context table for dependencies**: Added columns for Risk (exploitability), Used in (component), and License compatibility
- **License compatibility check**: Flag GPL/MIT/Apache conflicts with project license
- **Dev vs Prod classification**: Detect build tools in dependencies instead of devDependencies
- **End-of-life detection**: Warn on packages last updated >2 years ago
- **Lockfile freshness check**: Flag stale lockfiles (>6 months) for regeneration

#### Duplication Detection
- **Extraction cost analysis**: Assess whether extracting duplication is worth it (cost vs benefit)
- **Severity levels**: High-pain (5+ places), Medium-pain (3-4), Low-pain (2-3)
- **Eligible patterns clarified**: Validation, API calls, error handling, type guards, formatting
- **Skip criteria**: Coincidental similarity, domain-specific logic, single-use code, brittle coupling

#### Triage & UX
- **Triage summary**: Executive snapshot (findings count, severity breakdown, effort estimates)
- **Quick wins identification**: < 5 minute fixes highlighted
- **Context mode selection**: Startup (ship fast) vs Enterprise (comprehensive) vs Learning (explain why)
- **Quick commands**: Narrow scope (security only, one file, branch compare, etc.)

#### Pass 2 Improvements
- **Pre-flight checklist**: Files to modify, behavior changes, risk level assessment before any edits
- **Verification post-fix**: Build, test, linter, lockfile diff, behavior changes, accidental refactoring
- **Step-by-step guidance**: Before/after snippets for each fix type

### 🔧 Changed

- **Step 0 — Stack check expanded**: Now includes detailed test coverage breakdown, build system, CI/CD, Docker, and key assumptions
- **Pass 1 organization**: Added intra-section sorting (by CVSS, exploitability, maintenance pain)
- **Security section**: Reorganized into clear subsections with exhaustive checklist
- **Tone guidance**: Match user framing, adapt to context mode (startup vs enterprise vs learning)

### 📚 Documentation

- Added comprehensive README.md with quick start, feature list, and example flow
- Added CHANGELOG.md (this file) for version tracking
- Added package.json for npm distribution
- Expanded all section descriptions with concrete examples

### 🚀 Quality Improvements

- **No safety theater**: Explicit guidance on when to say "safe" (only with test evidence)
- **Context before judgment**: Recommendations now adapt to user's constraints (startup, enterprise, learning)
- **Practical focus**: Smallest change that solves the problem; no abstractions user didn't ask for
- **Transparency**: Behavior changes explained explicitly; major upgrades flagged but not applied

---

## [1.0.0] — 2023-12-XX

### ✨ Added

- Initial two-pass audit workflow
- Pass 1: Find & Report (Security, Dependencies, Duplication)
- Pass 2: Fix (Security fixes, Dependency updates, Safe cleanups)
- Core principles: two passes, no safety theater, smallest changes, don't touch business logic
- Step 0: Stack check (language, framework, tests)
- Security checks: secrets, input validation, auth, sensitive data, unsafe code, CORS
- Dependency scanning: vulnerability audit, version tracking
- Duplication detection: copy-pasted logic flagging
- Closing summary: concrete recap of all changes
- Tone guidance: direct, practical, tables over prose

---

## Format Notes

- **Security findings**: Sorted by severity (Critical > High > Medium > Low)
- **Dependency findings**: Vulnerable with fix > Vulnerable no fix > Transitive > Outdated > License issues
- **Duplication findings**: High-pain > Medium-pain > Low-pain
- **All findings**: Include file:line, why it matters, suggested fix

---

## Contributing

See README.md for contribution guidelines.

---

**Last updated**: 2024-01-XX  
**Maintained by**: freemind25
