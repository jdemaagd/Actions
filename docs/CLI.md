# CLI

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
- gh variable delete ACTIONS_STEP_DEBUG

## Resources

- [GitHub CLI](https://cli.github.com/)
