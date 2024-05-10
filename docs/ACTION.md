# GitHub Actions

## Docker

- docker run $(docker build -q .)
- docker run $(docker build -q .) foo bar

## Actions

- Docker container actions
    - run on Linux only
    - contain all their dependencies in the container
    - slower because of time to retrieve/build image and start container
- JavaScript actions
- Composite actions

## TypeScript action template

- npm install
- npm test
- npm run bundle > run every time .ts file is modified
- npx prettier . --check
- npx prettier . --write

## Act with Docker

- act pull_request -l > list all workflows and jobs for corresponding trigger
- act pull_request -n > perform dry run
- act pull_request > execute workflow in container
- act -s GITHUB_TOKEN=[insert personal access token]
- act -s GITHUB_TOKEN="$(gh auth token)"
- create ~/.actrc
    - add this line > `--container-daemon-socket -`

## Resources

- [Act: run workflow locally](https://github.com/nektos/act)
- [Install Act](https://nektosact.com/)
- [TypeScript Action](https://github.com/actions/typescript-action)
