# AI DevOps Rules

**Version 1.3.0** | Comprehensive rules for AI coding assistants in DevOps workflows

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

> "Partnership without honesty is just convenient automation."

Born from a meta-experiment where AI peer-reviewed its own rules—and a human caught what three AI models missed. 

**Read the full story:** [I Work With AI Every Day. That's Why I Missed What It Couldn't See.](https://medium.com/@yair.talor/i-work-with-ai-every-day-thats-why-i-missed-what-it-couldn-t-see-e5a684bfe324)

---

## What This Is

A `.cursorrules` file that transforms AI coding assistants (Cursor, Continue, etc.) from yes-men into partners that actually challenge you.

Built specifically for DevOps engineers working with:
- Terraform/Terragrunt
- Kubernetes/Helm/Helmfile  
- AWS/Azure/GCP
- Python/Go automation
- CI/CD pipelines
- GitLab/GitHub workflows

## Why It Exists

AI assistants are helpful. But they also:
- ❌ Suggest non-existent APIs
- ❌ Ignore your repo's established patterns
- ❌ Don't question dangerous commands (like pushing to main)
- ❌ Act like yes-men instead of partners

**These rules fix that.**

## The Problem We Solved

We spent hours building comprehensive AI rules. Two instances of Claude Sonnet 4.5 peer-reviewed each other. Gemini 2.0 Pro reviewed them too.

All three missed: **"Don't push to main."**

That moment taught us:
- **Technical rules** → AI can peer-review brilliantly
- **Cultural rules** → Only humans can define

Both are needed for a real partnership.

---

## Quick Start

### For Cursor Users

1. **Copy to your project:**
```bash
   curl -o .cursorrules https://raw.githubusercontent.com/yairt2/ai-devops-rules/main/.cursorrules
```

2. **Or add to User Rules:**
   - Open Cursor Settings
   - Go to "Rules for AI"
   - Paste contents of `.cursorrules`

3. **Let AI create context:**
   - AI will offer to create `.cursor/PROJECT_CONTEXT.md`
   - This captures your repo's patterns
   - Say yes (takes ~30 seconds)

4. **Start working:**
   - AI now challenges complexity
   - Validates APIs before suggesting
   - Catches cultural violations (like pushing to main)
   - Matches your repo's patterns

### For Other AI Assistants

These rules are designed for Cursor but work with any AI coding assistant that supports custom rules. Adapt the format to your tool's configuration system.

---

## What's Inside

### Quick Reference (8 Critical Actions)
1. Check `.cursor/PROJECT_CONTEXT.md` first
2. Use context7 MCP to verify APIs
3. Always use awsume for AWS/kubectl
4. Never push to master/main
5. Ask guiding questions when unclear
6. Search GitHub/Stack Overflow first
7. Maximum scrutiny for production changes
8. Jira defaults: CLOUDEVOPS, Task, assignee

### Core Principles (6 Rules)
1. Respect existing patterns
2. Start simple (KISS)
3. Challenge decisions with evidence
4. Elegant first, pragmatic second
5. Validate everything
6. Infrastructure as Code

### Workflow Requirements
- **Git:** Branch-based workflow, never push to main
- **AWS:** awsume profile management
- **IaC:** No manual kubectl/aws cli unless emergency
- **Pattern Detection:** Auto-scan repos via PROJECT_CONTEXT.md

### The Missing Piece: Cultural Rules
The "obvious" things AI can't infer:
- Team conventions
- Code review standards  
- Deployment rituals
- The unwritten rules

---

## How It Works

### 1. Pattern Detection
AI checks for `.cursor/PROJECT_CONTEXT.md` on first interaction:
```
Before I help with [task], should I create a PROJECT_CONTEXT.md file?
(Quick scan: ~30sec, recommended for pattern consistency)
```

This captures:
- Directory structure
- Naming conventions
- Tool versions
- IaC patterns
- Code style

### 2. Validation Protocol
Before suggesting code, AI:
- ✅ Checks context7 MCP for latest docs
- ✅ Verifies APIs/functions exist
- ✅ Searches for existing solutions
- ✅ Matches repo patterns
- ✅ Ensures IaC backing

### 3. Challenge System
AI pushes back when:
- Solution is overcomplicated (KISS violation)
- Security/scalability red flags detected
- Better patterns exist with evidence
- Missing critical workflow steps (awsume, branches)
- Deviating from repo patterns without justification

### 4. Maximum Scrutiny Mode
Auto-activates on keywords: `production`, `critical`, `security`, `compliance`, `scale`

When triggered:
- Questions every assumption
- Verifies against official sources
- Checks security implications
- Validates monitoring/rollback plans
- Demands "will work because..." not "should work"

---

## The Evolution

**v1.0.0** → Initial comprehensive rules  
**v1.1.0** → Added Quick Reference, reduced redundancy 30%  
**v1.1.1** → Git workflow protection (the human-caught gap)  
**v1.2.0** → PROJECT_CONTEXT.md pattern detection  
**v1.2.1** → Consolidated for clarity  
**v1.3.0** → Non-blocking pattern suggestions, improved UX  

Full version history in `.cursorrules` file.

---

## Customization

### For Your Team
1. Fork this repo
2. Update Jira defaults (project, issue type)
3. Add your team's cultural rules
4. Modify tool list for your stack
5. Adjust challenge thresholds

### For Your Stack
Not using Terraform? Replace with your IaC tool.  
Not using awsume? Replace with your auth method.  
Different git workflow? Update branch rules.

**The principles remain the same.**

---

## Examples

### Before Rules
```
You: "push this to prod"
AI: *executes git push to main*
```

### After Rules
```
You: "push this to prod"
AI: "STOP. You're on main. Never push to master. Create a branch first:
     git checkout -b feature/your-change
     
     Also, I see this touches production config. Have you:
     - Verified this in staging?
     - Updated IaC (Terraform)?
     - Checked with the team?"
```

---

## Contributing

Found a blind spot we missed? **PR welcome.**

We're still learning what AI can't see without being told.

### What to Contribute
- New cultural rules we missed
- Tool-specific patterns
- Challenge scenarios
- Real-world failures these rules would catch

### What NOT to Contribute
- Tool-specific implementations (keep it general)
- Personal preferences without reasoning
- Rules that conflict with core principles

---

## The Story Behind This

Read the full article: [I Work With AI Every Day. That's Why I Missed What It Couldn't See.](https://medium.com/@yair.talor/i-work-with-ai-every-day-thats-why-i-missed-what-it-couldn-t-see-e5a684bfe324)

**TL;DR:** We used AI to build AI rules. It worked brilliantly for technical stuff. Then a human teammate caught what three AI models missed: "Don't push to main."

That taught us about cultural blindness in AI, the danger of working too closely without boundaries, and why partnership requires honesty.

---

## License

MIT License - Use it, adapt it, make it yours.

## Author

**Yair Tal-Or** | DevOps Engineer

Working shoulder to shoulder with AI daily, learning where it excels and where it needs human guidance.

---

## Acknowledgments

- Claude Sonnet 4.5 (peer reviewer)
- Cursor AI (peer reviewer)  
- Gemini 3.0 Pro (explaining why we all failed)
- My teammate (catching what we missed)

Partnership means knowing each other's limitations.

---

**Current Version:** 1.3.0  
**Last Updated:** November 30, 2025  
**Status:** Production-ready, actively maintained