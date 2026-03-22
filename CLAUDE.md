# Claude Code Configuration

## gstack

This project uses [gstack](https://github.com/garrytan/gstack) for development workflows and tooling.

### Web Browsing

- **Always use `/browse` skill from gstack for all web browsing**
- Never use `mcp__claude-in-chrome__*` tools

### Available Skills

- `/office-hours` — Schedule and manage office hours
- `/plan-ceo-review` — Plan CEO review
- `/plan-eng-review` — Plan engineering review
- `/plan-design-review` — Plan design review
- `/design-consultation` — Get design consultation
- `/review` — Code review
- `/ship` — Ship code to production
- `/land-and-deploy` — Land and deploy changes
- `/canary` — Run canary deployments
- `/benchmark` — Run benchmarks
- `/browse` — Browse the web (use this for all web browsing)
- `/qa` — QA and testing
- `/qa-only` — QA only
- `/design-review` — Design review
- `/setup-browser-cookies` — Setup browser cookies
- `/setup-deploy` — Setup deployment
- `/retro` — Retrospective
- `/investigate` — Investigate issues
- `/document-release` — Document release
- `/codex` — Code exploration and analysis
- `/careful` — Careful/cautious mode
- `/freeze` — Freeze deployments
- `/guard` — Guard mode
- `/unfreeze` — Unfreeze deployments
- `/gstack-upgrade` — Upgrade gstack
