WORKFLOW FIXES — ScubaGear

Summary of findings
- Multiple CodeQL Advanced workflow runs are failing at startup (conclusion: startup_failure). Example run: https://github.com/TechnicallyIncorrect1/ScubaGear/actions/runs/28653974186

Likely causes
- Repository or organization Actions permissions blocking workflow startup.
- Workflows originating from a fork may require first-run approval.
- Marketplace actions used by the workflow may be disallowed by org policy.

Required admin actions (please perform or allow me to re-check after you do):
1. Settings → Actions → General
   - Ensure Actions are enabled for this repository.
   - Under "Allow actions and reusable workflows", either allow all actions or ensure the specific actions used (github/codeql-action/*, actions/checkout@v4) are allowed.
2. If this repo is a fork: review the "Allow GitHub Actions from forks" / approve first-run workflows.
3. Check for self-hosted runners: Settings → Actions → Runners — confirm runners are online and labelled correctly if workflows require them.
4. After settings change, re-run the failing workflow(s) and share logs if startup issues persist.

Secrets needed for publish workflows (if used)
- PYPI_TOKEN (if publishing to PyPI)
- GPG_PRIVATE_KEY and GPG_PASSPHRASE (if you sign packages)

What I prepared on the branch
- This WORKFLOW_FIXES.md describing required admin steps
- .github/workflow-fixes/SUGGESTED_CODEQL.yml containing a minimal CodeQL config to simplify language detection and reduce startup failures

Next steps I can take once you confirm the admin changes or add secrets
- Open a follow-up PR to update workflows to pinned actions and pre-flight checks
- Re-run workflows and fix any remaining job-level errors

If you want me to proceed to create a PR with workflow changes, confirm and I will prepare the exact workflow edits.