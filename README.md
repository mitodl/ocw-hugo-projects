# ocw-hugo-projects

A collection of Hugo project templates for different types of OCW
websites

## linting and formatting

We have a YAML linting and formatting setup in this repo to ensure that, at the
least, our checked-in files are valid YAML files.

To install dependencies you'll want to do something like the following:

```sh
yarn install # install prettier
virtualenv env
source env/bin/activate
pip install -r requirements.txt # install yamllint
```

Then you can run the linter by doing

```sh
yamllint .
```

And run the formatter with

```sh
yarn fmt
```

These checks are run on PRs by GitHub actions as well.
