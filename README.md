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
