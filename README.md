# misleading-name-check

GitHub Actions that checks whether a provided name is misleading or not.

## Usage

You can check whether `name` is misleading or not by comparing it with strings in `list`.
This action will output `is-misleading` so that you can extract the result afterward.

### Example workflow

```yaml
name: Test

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  misleading:
    runs-on: ubuntu-latest
    steps:
      - id: check-misleading
        uses: ken-matsui/misleading-name-check@main
        with:
          name: aaaa
          list: aaab aaabc

      - name: Test the result
        run: |
          [ '${{ steps.check-misleading.outputs.is-misleading }}' = 'true' ]
```

### Inputs

* `name` (required): A name to check
* `list` (required): A list of words to check
* `version`: A version of [`suggestion-cli`](https://github.com/ken-matsui/suggestion-cli) (default is `latest`)
* `distance`: Levenshtein distance if needed (default is `1`)

### Outputs

* `is-misleading`: A string output, either `true` or `false`.

## Contribution

Contributions, including issues and pull requests, are very welcome.
