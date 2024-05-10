# Share Action on Marketplace

## Draft Release

- GitHub detects action.yml file
    - proposes to publish release in a blue banner
    - same as going to `Releases` and clicking `Draft a new release`
- In dialogue, there are some warnings to help improve marketplace listing
    - click on link for available icons and colors and pick one of each
- Open `action.yml` file and add branding and author information
- A good `README.md` file is important for marketplace listing
    - add section for inputs, outputs, and usage example
- Commit and push changes
- Go back to browser and refresh new release window
- Click `Choose a tag`, enter v1.0
    - click `Create new tag`
- Add `v1.0` as title of release
    - can automatically generate release notes for release
    - however, results will only be very good if working with pull requests
    - can also add a description manually
- Click `Publish release`
    - in release, see `Marketplace` and `Latest` labels
- Click `Marketplace` label
    - brings you to marketplace listing

## Semantic Versioning (`<major>.<minor>.<patch>-<pre>`)

- Major version
    - numeric identifier that gets increased if version is not backward-compatible and has breaking
      changes
    - an update to a new major version must be handled with caution!
    - major version of zero is for initial development
- Minor version
    - numeric identifier that gets increased if new features are added
    - version is backward-compatible with previous version and can be updated without breaking
      anything if you need new functionality
- Patch
    - numeric identifier that gets increased if you release backward-compatible bug fixes
    - new patches should always be installed
- Pre-version
    - text identifier that is appended using a hyphen
    - identifier must only use ASCII alphanumeric characters and hyphens ([0-9A-Za-z-])
    - the longer the text, the smaller the pre-version (meaning -alpha < -beta < -rc)
    - pre-release version is always smaller than a normal version (1.0.0-alpha < 1.0.0)

## Resources

- [README Example](https://github.com/wulfland/DockerActionRecipe)
- [Semantic Versioning](https://semver.org/)
