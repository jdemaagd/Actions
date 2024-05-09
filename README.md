# GitHub Actions - Deep Dive

## Pricing

- Public repos: unlimited minutes for actions
- Self-hosted runners: free
- GitHub-host runners
    - Linux > $0.008 per minute
    - Windows > $0.080 per minute
    - MacOS > $0.160 per minute
- NOTE: actions consumes storage for logs, workflow artifacts, caching, etc.
    - billed $0.008 per GB per day if included storage is exceeded

## Marketplace

- Search > Most installed/starred, Best Match, or Recently added

## Shell

- non-Windows: bash > sh (fallback)
- Windows: powershell core (pwsh) > cmd (fallback)

## Triggers

- Manual
- Webhook: start workflow based on an event in GitHub
- Scheduled: run workflow at multiple scheduled times (cron syntax)

```yaml
on:
  schedule:
    # Runs at every 15th minute
    - cron: '*/15 * * * *'
    # Runs every hour from 9am to 5pm
    - cron: '0 9-17 * * *'
    # Runs every Friday at midnight
    - cron: '0 2 * * FRI'
```

## Hierarchy

- Organization > Repository > Environment

## GitHub CLI Commands

- git switch -c new-workflow
- gh secret set secret-name
- gh variable set var-name
- gh secret set secret-name < secret.txt
- gh variable set var-name --body config-value
- gh secret set secret-name --env environment-name
- gh secret set secret-name --org org -v private
- gh secret set secret-name --org org -v selected -r repo
- gh pr create --fill
- gh variable set ACTIONS_STEP_DEBUG --body true

## Injection Attack

- Creating PR > "Hi";ls $GITHUB_WORKSPACE;echo "-"
- Executes following command > echo "Hi";ls $GITHUB_WORKSPACE;echo "-"
- Script `ls $GITHUB_WORKSPACE` will execute without error
- from there, you can find other ways to inject more harmful script

## Debugging

- debug: only message that cannot annotate files
- workflow command only accepts message as a parameter

## Resources

- [GitHub CLI](https://cli.github.com/)
- [GitHub Marketplace](https://github.com/marketplace)
- [Workflow Triggers](https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows)
