# Release Pipeline Template

Use this release flow as a portable baseline for CI/CD across GitHub Actions, GitLab CI, Azure Pipelines, Jenkins, or another runner.

## Pipeline stages

1. **Validate source**
   - Install dependencies
   - Run lint, typecheck, and unit tests
2. **Build artifact**
   - Compile or package the backend
   - Build container image if the runtime uses containers
3. **Verify contract**
   - Run API or smoke checks against the packaged artifact
   - Verify environment-specific config is present
4. **Deploy**
   - Apply manifests or publish the release artifact
   - Run migrations in a controlled step
5. **Post-deploy validation**
   - Run smoke checks against the live environment
   - Confirm health, readiness, and key error-rate signals
6. **Rollback trigger**
   - Stop rollout or restore the previous version if validation fails

## Gating rules

- Do not deploy from an untagged or unreviewed artifact if the team requires release traceability.
- Do not mark deploy success before smoke checks pass.
- Treat migration failures, readiness failures, or elevated error rates as rollback candidates.
