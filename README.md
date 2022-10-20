# Release Notes Action

Generate release-notes for a given version from a CHANGELOG file.

## Usage

```yaml
steps:
  - uses: actions/checkout@v3

  - id: release-notes
    uses: freckle/release-notes-action@v1
    with: # All optional, defaults shown
      file: ./CHANGELOG.md
      version: ""
      version-header-regex: '^## \[(v?[0-9.]+[^]\s]*)]'

  - uses: actions/create-release@v1
    id: create-release
    with:
      body_path: ${{ steps.release-notes.outputs.path }}
      # ...
```

## Inputs

- **file**: Path to the CHANGELOG

  Default is `./CHANGELOG.md`.

- **version**: Version to locate

  Default is empty which means first (assumed to be latest)

- **version-header-regex**: Regular expression used to match headers.

  This regular expression should match only version section-headers, and capture
  the version itself as the first capture group.

  The default matches level-2 markdown headers containing a version-like string
  as a link:

  ```
  version-header-regex = /^## [({version})].*/

  version = /v?[0-9.]+{suffix}/

  suffix = /[^]\s]*/
  ```

## Outputs

- **path**: Path to a temporary file where the content was written

## FAQ

> What if my CHANGELOG isn't in the right format?

Adjust `version-header-regex` as necessary.

> How can I check if release-notes were successfully generated?

```sh
if [[ -s "${{ steps.release-notes.outputs.path }}" ]]; then
  echo "Release notes were generated"
fi
```

> How can I get the release notes as a string?

```sh
notes=$(< "${{ steps.release-notes.outputs.path }}")
```

---

[LICENSE](./LICENSE)
