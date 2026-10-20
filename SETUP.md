# Setup guide — Bhavesh's GitHub profile

## Files

- `README.md` — profile layout.
- `.github/workflows/metrics.yml` — scheduled Lowlighter Metrics workflow.

## 1. Put these files in your profile repository

Your profile repository must be named exactly `bhaveshnerkar` and live at:
https://github.com/bhaveshnerkar/bhaveshnerkar

Copy `README.md` to the repository root. Copy the `.github/workflows/metrics.yml` file to the same path in that repository.

If your default branch is not `main`, change `committer_branch: main` in both workflow steps to your actual default branch.

## 2. Add the Metrics token as a secret

Lowlighter Metrics documentation says a personal access token is needed for user activity data that a repository-scoped `GITHUB_TOKEN` cannot read. Create a fine-grained or classic personal access token in GitHub settings, using the smallest permissions that work for the selected public-data plugins. For a classic token, the official setup guide says no scopes are required by default; some plugins/features may require extra scopes. Do not add private repository access unless you intentionally need it.

Then go to your profile repository:
Settings → Secrets and variables → Actions → New repository secret

Name: `METRICS_TOKEN`
Value: paste the token.

Never put the token directly in README.md or the workflow file. Do not share it in chat or commit it to Git.

## 3. Confirm Actions permissions

The workflow grants only `contents: write`, needed for the action to commit the generated SVG files to this same repository. `GITHUB_TOKEN` is passed as `committer_token`; `METRICS_TOKEN` is used for reading profile metrics. If your repository or organization policy disables write access for Actions, enable read/write workflow permissions in repository Settings → Actions → General, if allowed.

## 4. Optional AniList section

The anime card is optional. In your repository, go to:
Settings → Secrets and variables → Actions → Variables → New repository variable

Name: `ANILIST_USERNAME`
Value: your AniList username (not your password or token).

The workflow will skip the AniList step while the variable is blank. Once set, it will generate `metrics.anilist.svg`. The AniList plugin documents that this plugin needs no token for public AniList data.

If you don't use AniList, delete the anime section from README.md and remove the optional AniList step from the workflow.

## 5. Run the workflow

Open the repository's Actions tab → `Update GitHub Profile Metrics` → `Run workflow`.

Wait for it to finish, then refresh your profile. The generated files `github-metrics.svg` and, if configured, `metrics.anilist.svg` should appear in the repository.

## Notes

- The 3D-style contribution calendar is the isometric calendar plugin, not a guarantee of a fully animated GitHub Skyline scene.
- The external stats cards in README.md may occasionally be rate-limited or unavailable because they are hosted by third-party services.
- `uses: lowlighter/metrics@latest` follows the latest stable action tag. For stricter supply-chain pinning, review the official repository and pin a verified release or commit SHA.
- If the workflow fails, open its log in Actions. Common causes are a missing `METRICS_TOKEN`, a branch name mismatch, or Actions write permissions being disabled.
