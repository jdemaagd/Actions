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

## Injection Attack

- Creating PR > "Hi";ls $GITHUB_WORKSPACE;echo "-"
- Executes following command > echo "Hi";ls $GITHUB_WORKSPACE;echo "-"
- Script `ls $GITHUB_WORKSPACE` will execute without error
- from there, you can find other ways to inject more harmful script

## Debugging

- debug: only message that cannot annotate files
- workflow command only accepts message as a parameter

## Resources

- [GitHub Marketplace](https://github.com/marketplace)
- [Workflow Triggers](https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows)
