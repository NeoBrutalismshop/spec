# NeoBrutalismshop — GitHub and restoration guardrails

## Mandatory safety boundaries
- GitHub Actions must remain disabled in this repository. Do not enable or dispatch workflows, including historical workflow YAML restored as inert source.
- Do not run autonomous agents, scraping/crawling, general computing, scheduled business automation, third-party website interactions, or persistent workers on GitHub-hosted infrastructure.
- Use an authorized local computer or controlled VPS for builds, tests, and site generation. Push reviewed commits and static assets deliberately; verify live behavior separately.
- Do not force-push, rewrite restoration history, overwrite verified backups, or bulk-import historical branch snapshots with unknown merge state.
- Never add real passwords, personal data, secrets, auth tokens, signing material, or private license keys to source or logs.
- Preserve the public/private boundary: neolicenser-pro is private and must not be copied to public repositories.
- Treat original pre-recovery Git SHAs as archival provenance. API source snapshots cannot re-create PRs, reviews, releases, or full historical Git commit ancestry.
- Inspect and verify historical workflows before contemplating use. Existing workflows are disabled and not release authority.

## Repository recovery
See RESTORE-STATUS.md. The first new commit retains the archived source tree exactly; later changes are new reviewed restoration or rebranding commits.
