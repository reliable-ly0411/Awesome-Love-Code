# Upstream automation policy

- Daily and manual source sync follows `sun0225SUN/Awesome-Love-Code:main` into `sync-only/upstream-main`. It does not build or publish.
- Local workflows and maintenance policy are retained; conflicting upstream changes stop rather than force-push.
- Existing historical tags and releases are never recreated or overwritten. Baseline deployment does not backfill releases.
- No recognized new upstream formal release means no automatic heavyweight build or publication. A source commit, website rebuild, tag alone, or dependency update is not a release signal.
- Manual build and promotion remain separate where the repository has a real deliverable. Repositories without a build/publisher do not gain a fabricated release route.
- Lightweight read-only safety checks remain enabled. This policy does not enable third-party dispatch, credentials, external AI, or repository security settings.
- Website repositories sync into a non-publishing source branch. Publication requires an explicit manual promotion of verified build artifacts; no automatic merge into the live Pages source.

## Manual website operations

The current live site uses GitHub Pages `main` / root with the Cayman Jekyll theme. A default-branch policy merge would itself cause a branch-based deployment. Keep the policy PR unmerged until migration to GitHub Actions mode is explicitly approved; preserve the existing live site and do not rebuild or republish during that migration.

After that prerequisite, run `site-build.yml` manually on the default branch with a full source commit SHA. It uses GitHub's Jekyll Pages builder and stores an immutable `site-candidate` for 30 days. The separate `site-promote.yml` verifies the exact build run, source SHA, tooling SHA and original tar SHA256, then deploys those same bytes without rebuilding. Its read-only preflight requires Pages to already use workflow mode and never enables or reconfigures the site. Expired or inconsistent artifacts are rejected rather than rebuilt.
