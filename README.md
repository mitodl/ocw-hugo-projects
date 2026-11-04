# ocw-hugo-projects

A collection of Hugo project templates for different types of OCW
websites

## Releasing

Releases are tags only. There is no `release` or `release-candidate` branch to merge into: the Concourse release workflow cuts a release from `main`, and the `/doof` Slack command drives it. The steps are the same as for [`ocw-hugo-themes`](https://github.com/mitodl/ocw-hugo-themes#releasing), with `ocw-hugo-projects` in place of `ocw-hugo-themes` and `#doof-ocw-hugo-projects` as the channel. The general workflow is on the [Concourse release workflow handbook page](https://engineering.ol.mit.edu/handbook/delivering/release-process/concourse-release-workflow/).

What matters for this repo:

- A version is a calendar version, `YYYY.M.D.N`, for example `2026.11.5.1`. It lives in `VERSION` and the release workflow bumps it. Do not edit it by hand.
- The starter configurations (`*/ocw-studio.yaml`) reach `ocw-studio` through tags. A release tag (`2026.11.5.1`) is what CI and QA follow. A `production/` tag (`production/2026.11.5.1`) is what production follows, and only the workflow creates one, after the release issue is approved and closed. Merging to `main` does not change what any environment uses.
- Pushing a tag makes GitHub call the `ocw-studio` starter webhook, which syncs every `ocw-studio.yaml` at that tag, but only when it is the newest matching tag. Nothing is built or deployed by the release itself. See [Following release tags](https://github.com/mitodl/ocw-studio#following-release-tags-of-ocw-hugo-themes-and-ocw-hugo-projects) in the `ocw-studio` README.
- To cut a release: merge to `main`, run `/doof preview ocw-hugo-projects`, then `/doof release ocw-hugo-projects`. Check your boxes in the release issue, then promote with the button, `/doof promote ocw-hugo-projects`, or by closing the issue. To confirm a promotion, check that the `production/<version>` tag exists: `git ls-remote --tags origin 'production/*'`.
- The same commands as for `ocw-hugo-themes` apply: `release-status`, `release-notes`, `release ... supersede <version>`, `abandon` and `hotfix`.
- Release notes are in `CHANGELOG.md`, which each release updates. `RELEASE.rst` is no longer updated.
- Never create or move a release or `production/` tag by hand.

## linting and formatting

We use [prek](https://prek.j178.dev/) to ensure that, at the
least, our checked-in files are valid YAML files. It reads `.pre-commit-config.yaml`.

Install the version pinned in `.github/workflows/autofix.yml`:

```sh
uv tool install prek==0.5.3
prek install -f
```

`prek install -f` replaces an existing pre-commit git hook, if one is installed.

Then you can run the hooks by doing

```sh
prek run --all-files
```

To run only some hooks e.g for the formatter only

```sh
prek run yamlfmt --all-files
```

The `prek` check runs these hooks on PRs and pushes to `main` through GitHub
Actions. On PRs, when the hooks' own fixes make every hook pass,
[autofix.ci](https://autofix.ci/) pushes them as one commit. It refuses fixes to
files under `.github/`, so fix those locally.
