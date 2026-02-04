# ocw-hugo-projects

A collection of Hugo project templates for different types of OCW
websites

## linting and formatting

We use pre-commit to ensure that, at the
least, our checked-in files are valid YAML files.

To set up pre-commit you'll want to do something like the following:

```sh
pip install pre-commit
pre-commit install
```

Then you can run the pre-commit hooks by doing

```sh
pre-commit run --all-files
```

To run only some hooks e.g for the formatter only

```sh
pre-commit run yamlfmt --all-files
```

These checks are run on PRs by GitHub actions as well.
