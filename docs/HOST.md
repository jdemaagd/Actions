# Self-Hosted Runners

## Host in Container

- docker info | grep Architecture > x86_64
- docker run -it ubuntu:latest /bin/bash
- mkdir actions-runner && cd actions-runner
- apt-get -y update; apt-get -y install curl
- curl -o actions-runner-linux-arm64-2.316.1.tar.gz -L https://github.com/actions/runner/releases/download/v2.316.1/actions-runner-linux-arm64-2.316.1.tar.gz
- tar xzf ./actions-runner-linux-arm64-2.316.1.tar.gz
- ./bin/installdependencies.sh
- export RUNNER_ALLOW_RUNASROOT="1"
- ./config.sh --url https://github.com/{OWNER}/{REPO} --token {TOKEN}
- ./config.sh remove --token {TOKEN}
- ./config.sh --url {URL} --token {TOKEN} --ephemeral

## Dockerfile

- docker build -t simple-ubuntu-runner .
- docker run -d --rm -e RUNNER_NAME=Runner1 -e TOKEN={TOKEN} simple-ubuntu-runner

## Authentication

```
$ curl -L \
> -X POST \
> -H "Accept: application/vnd.github+json" \
> -H "Authorization: Bearer <YOUR-PAT>" \
> -H "X-GitHub-Api-Version: 2022-11-28" \
> https://api.github.com/repos/{OWNER}/{REPO}/actions/runners/registration-token

$ TOKEN=$(<curl command> | jq .token --raw-output)
```

## Cleanup

- docker system prune --force
- docker volume prune --force
