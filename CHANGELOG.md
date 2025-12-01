## [1.4.0] - 2025-12-01

### Changed
- **BREAKING:** Split rules into lightweight `.cursorrules` + `.cursor/DEVOPS_STANDARDS.md`
- Reduced token usage by 60% (~2,500 tokens vs 7,150 tokens per turn)
- Moved detailed processes to DEVOPS_STANDARDS.md (referenced when needed)
- Removed version history from rules files (now tracked in CHANGELOG.md)

### Why
- AI peer review identified token cost as optimization opportunity
- Faster responses, lower costs, same comprehensiveness
- Easier maintenance (update standards without touching core rules)

### Migration
- Replace `.cursorrules` with new version
- Create `.cursor/DEVOPS_STANDARDS.md` in your repo
- Claude will reference standards file automatically when needed