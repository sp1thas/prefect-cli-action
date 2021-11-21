# prefect Github Action

It requires that the [`checkout`][github-checkout] and [`setup-python`][github-setup-python] actions be used first.

## Inputs

 - `api-key` _(Required)_: A Prefect Cloud API key.
 - `project-name` _(Required)_: The name of the Prefect project to register this flow in.
 - `prefect-version` _(Optional)_:  Version of prefect to use
 - `flow-path` _(Optional)_: A path to a file or a directory containing the flow(s) to register
 - `flow-module-path` _(Optional)_: A python module name containing the flow(s) to register
 - `json-path` _(Optional)_: A path or URL to a JSON file created by `prefect build` containing the flow(s) to register
 - `flow-name` _(Optional)_: The name of a flow to register from the specified paths/modules. If provided, only flows with a matching name will be registered
 - `flow-label` _(Optional)_: A label to add on all registered flow(s)
 - `requirements-files` _(Optional)_: Path(s) to requirements files that should be installed to properly configure third-party imports

## Outputs

 - `prefect-result`: Output of the `prefect register` CLI.

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
      - uses: sp1thas/prefect-action@main
        with:
          apiKey: ${{ secrets.PREFECT_APIKEY }}
          projectName: test
          flowPath: flows/flow.py
```
