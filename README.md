# Prefect CLI Github Action

It requires that the [`checkout`][github-checkout] and [`setup-python`][github-setup-python] actions be used first.

## Inputs

 - `api-key` _(Required)_: A Prefect Cloud API key
 - `command` _(Required)_: The prefect command
 - `prefect-version` _(Optional)_:  Version of prefect to use
 - `requirements-files` _(Optional)_: Path(s) to requirements files that should be installed to properly configure third-party imports

## Outputs

 - `prefect-command`: Output of the prefect command

## Example usage

```yaml
name: Register prefect flow
on:
  - push

jobs:
  register-using-flow-path:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: actions/setup-python@v2
        with:
          python-version: 3.8
      - uses: sp1thas/prefect-cli-action@main
        with:
          command: auth login --key ${{ secrets.PREFECT_APIKEY }}
      - uses: sp1thas/prefect-cli-action@main
        with:
          command: register -p flows/flow.py
```
