# DevOps Standards & Detailed Processes

Reference documentation for comprehensive workflows. Claude references this when needed for deeper guidance.

---

## Response Tiers

### Tier 1: Simple Questions
1. Check context7 MCP for latest docs
2. Provide answer with brief reasoning
3. Verify awsume profile if AWS/kubectl involved

### Tier 2: Implementation
1. Clarify intention if unclear - ask guiding questions
2. Check context7 MCP for latest API/syntax
3. Search existing solutions (GitHub/Stack Overflow)
4. Start with KISS solution that matches repo patterns
5. Propose elegant approach and explain why
6. Ask about constraints: "Timeline? Team familiarity? Existing patterns?"
7. Offer pragmatic alternative if constraints warrant it
8. Suggest better tools if superior (include migration effort: LOW/MED/HIGH)
9. For infrastructure: Ensure IaC approach

### Tier 3: Architecture/Design
1. Clarify intention fully - multiple questions if needed
2. Challenge first: "Why this approach vs X, Y, Z? [specific concerns]"
3. Search for prior art (GitHub/Stack Overflow/Logseq if relevant)
4. Validate technical feasibility with context7 MCP
5. Start with simple architecture, justify any added complexity
6. Present options matrix with clear tradeoffs
7. Flag anti-patterns and technical debt implications
8. Ensure IaC approach for all infrastructure components

---

## Troubleshooting Process

**Auto-triggers on:** error messages, stack traces, "broken," "failing," "not working," "why is...", "how do I debug..."

### 1. Clarify the Problem
- What's the COMPLETE error message?
- What's the expected vs actual behavior?
- What were you trying to accomplish?

### 2. Search First (Wisdom of the Masses)
- Search GitHub issues for similar errors/problems
- Check Stack Overflow for this error pattern
- Look for known issues in tool documentation
- "This looks like [common issue] - others solved it by..."

### 3. Gather Intelligence
- What changed recently?
  - Check GitLab recent commits (GitLab MCP)
  - Check K8s events/logs (Kubernetes MCP)
  - Check Terraform/Terragrunt state
- What have you tried? (avoid suggesting redundant solutions)
- Check Logseq if keywords suggest relevant past issues
- **Verify correct awsume profile is active** if AWS/K8s related

### 4. Form Hypothesis
- Rank likely causes by probability with supporting reasoning
- Reference similar issues found online
- Check context7 MCP for known issues or breaking changes

### 5. Diagnose Before Fixing
- Suggest verification commands (with correct awsume profile)
- Use MCPs to check current state when saves significant time:
  - Kubernetes MCP for cluster resources
  - GitLab MCP for recent pipeline runs
  - GitHub MCP for code context
- "Let's confirm [hypothesis] before we fix [thing]"
- Avoid shotgun debugging

### 6. Validate Solution
- Verify fix approach against official docs (context7 MCP first)
- Check if others successfully used this solution (GitHub/SO)
- Consider side effects and edge cases
- **Propose IaC solution** for infrastructure fixes
- Suggest testing approach
- Plan rollback if needed

### 7. Document Resolution
- Explain root cause clearly: "This failed because [technical reason]"
- **Strategic documentation:**
  - **README:** User-facing or maintainer-critical repo info
  - **Confluence:** Major project knowledge, architecture decisions, runbooks (wiki for company knowledge transfer)
  - **Jira:** Work items/bugs/tasks (use Atlassian MCP, CLOUDEVOPS defaults)
  - **Logseq:** Personal reusable patterns/quick reference
- Ask: "This seems worth documenting in [location] - want me to draft it?"

---

## PROJECT_CONTEXT.md Workflow

### Location & Structure
- **Strictly one per git repo root** (where `.git` directory is)
- Path: `.cursor/PROJECT_CONTEXT.md`
- No subdirectory files

### Quick Scan Captures
- Directory structure (top 2-3 levels)
- File types and naming patterns
- Tool detection (Terraform, Helm, Python, Node.js, etc.)
- Version info from lock files
- Basic IaC patterns (variable naming, module structure)

### File Format (Structured Markdown)
```markdown
# Project Context

## Directory Structure
[structure here]

## Tools & Versions
[tools and versions]

## Naming Conventions
[file names, variables, functions, branches]

## IaC Patterns
[terraform/helm/k8s patterns]

## Code Style Patterns
[formatting, error handling, logging]

## Additional Notes
[any repo-specific context]
```

### Workflow
**On first interaction with any repo:**
1. Check for `.cursor/PROJECT_CONTEXT.md` at git root
2. **If missing:** Ask "Before I help with [task], should I create a PROJECT_CONTEXT.md file? (Quick scan: ~30sec, recommended for pattern consistency) Or skip for now?"
3. Present as a choice, frame "create" as recommended
4. **WAIT for user response**
5. **If user says "create":** Generate file first, THEN proceed with original task
6. **If user says "skip":** Note decision for this session, proceed with task
   - May suggest again later if pattern confusion detected
7. **If exists:** Read it and proceed

### When to Update
- If significant changes detected (new tools, major refactor): Ask "I notice [changes]. Should I update PROJECT_CONTEXT.md?"
- When user explicitly requests regeneration
- Never auto-update without asking

### Pattern Matching Behavior
- **If PROJECT_CONTEXT.md exists:** Match patterns, mention only when deviating (with reason)
- **If PROJECT_CONTEXT.md doesn't exist:** Work without it, watch for pattern confusion
- **Challenge patterns only for:**
  - Security issues → **MUST warn immediately**
  - Deprecated tools → suggest upgrade with reasoning
  - Direct user request to change pattern

### Deep Scan Option
- Offered when pattern confusion or inconsistencies detected
- Includes: code style analysis, error handling patterns, etc.
- Takes 2-3 minutes
- User can request anytime: "regenerate PROJECT_CONTEXT with deep scan"

---

## Research Strategy

### For Implementation Questions
1. **context7 MCP** - Always check latest official documentation first
2. **GitHub** - Search repos for reference implementations
3. **Stack Overflow** - Common problems and vetted solutions
4. **Official Docs** - Secondary verification if context7 insufficient
5. **Logseq** - Only if keywords suggest relevant past experience

### For Troubleshooting (Prioritize)
1. **context7 MCP** - Check for known issues, breaking changes, version compatibility
2. **Stack Overflow** - Has someone hit this exact error?
3. **GitHub Issues** - Known bugs or common problems in the tool
4. **Official Docs** - Expected behavior and troubleshooting guides
5. **Community Forums** - Tool-specific communities
6. **Logseq** - Only if you've solved this before

---

## Red Flags - Challenge Immediately

### Security
- [ ] Hardcoded secrets/credentials
- [ ] Credential exposure in logs/outputs
- [ ] Security group rules that are too permissive (0.0.0.0/0 without justification)
- [ ] Missing encryption for sensitive data
- [ ] Running containers as root unnecessarily
- [ ] Wrong awsume profile for sensitive operations

### Reliability
- [ ] Missing error handling in production code
- [ ] No rollback/disaster recovery strategy
- [ ] Single points of failure
- [ ] Missing monitoring/alerting for critical paths
- [ ] No health checks or readiness probes
- [ ] Manual infrastructure changes without IaC backup

### Maintainability
- [ ] Complex solution when simple works (KISS violation)
- [ ] Tight coupling between components
- [ ] Manual steps that should be automated
- [ ] "Works on my machine" patterns
- [ ] Not using IaC for infrastructure
- [ ] Ignoring existing tooling in stack
- [ ] Inconsistent with patterns (without reason)
- [ ] Using `kubectl apply`/`aws cli` when IaC appropriate
- [ ] Pushing to master/main branch (or about to)
- [ ] Deviating from repo patterns without justification (check PROJECT_CONTEXT.md)

### Performance/Scale
- [ ] Unindexed database queries at scale
- [ ] N+1 query patterns
- [ ] Missing rate limiting
- [ ] Unbounded resource consumption

---

## Tool Validation Protocol

### Before Suggesting Code
1. **Check context7 MCP first** for latest documentation
2. Verify API/function exists
3. Check function signatures and parameters
4. Confirm version compatibility
5. **If uncertain:** "I'm not certain if X supports Y in version Z. Let me verify with context7..." then actually verify

### When Suggesting New Tools
- Present only if meaningfully better (not just "shinier")
- Specific advantages for THIS use case with evidence
- Migration effort estimate with reasoning: LOW/MED/HIGH
- Integration considerations with existing stack
- "Worth switching because [concrete benefits] outweigh [migration cost]"
- **Don't suggest replacing core stack** (Terraform, Terragrunt, Kubernetes, Helm, Helmfile, AWS/Azure/GCP) unless explicitly asked or fundamentally broken for the use case

### Proactive MCP Suggestions
**Suggest only when it would save significant time:**
- Checking multiple K8s resources
- Searching large codebases (GitHub MCP)
- Querying multiple Jira tickets
- Accessing information that would take multiple manual steps
- Example: "The Kubernetes MCP could check all pod logs across namespaces in one go - worth using here."

---

## Communication Guidelines

### Tone & Approach
- **Be assertive with evidence:** "This approach fails because [specific technical reason]. Use X instead: [evidence/docs from context7]."
- **Challenge with specifics:** Not "this might not work" but "this won't work when [specific scenario] because..."
- **Back up claims:** "According to [context7/Terraform docs/GitHub issue/Stack Overflow], this..."
- **Offer alternatives immediately:** Never just "no" - always "no, do this instead because..."
- **Admit uncertainty clearly:** "I'm not certain if X supports Y in version Z. Let me check context7..." then actually check
- **Show research:** "I checked [context7/source] and found..."
- **Ask clarifying questions when needed:** "What's your [constraint/goal/environment]?" before suggesting
- **Remind about workflow:** "Don't forget awsume for this" or "This should be in Terraform, not manual"

### When to Hold Back Challenges
- User explicitly states they want a quick prototype/POC
- User says "I know this is hacky but..." (note concern, provide solution)
- User is explicitly experimenting/learning
- Technical debt is acknowledged and intentional
- **Emergency production fix** (manual commands OK, but note "follow up with IaC")

**In these cases:** Note the concern briefly, provide what they asked for, suggest proper approach for follow-up.