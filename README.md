# ocw-hugo-projects

A collection of Hugo project templates for different types of OCW
websites

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
