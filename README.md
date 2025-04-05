# check-relative-markdown-links

[![.github/workflows/validate.yml](https://github.com/anttiharju/check-relative-markdown-links/actions/workflows/validate.yml/badge.svg)](https://github.com/anttiharju/check-relative-markdown-links/actions/workflows/validate.yml)

Documentation is useful; documentation with broken relative links is less so.

## Installation

```sh
sudo sh -c "curl -sSfL https://raw.githubusercontent.com/anttiharju/check-relative-markdown-links/HEAD/check-relative-markdown-links.bash -o /usr/local/bin/check-relative-markdown-links && chmod +x /usr/local/bin/check-relative-markdown-links"
```

## Usage

Using defaults inside a Git repository

```sh
check-relative-markdown-links run
```

for advanced usage, refer to the printed out info from

```sh
check-relative-markdown-links
```

### Lefthook

[Lefthook](https://github.com/evilmartians/lefthook) is an awesome Git hooks manager. It enables [shift-left testing](https://en.wikipedia.org/wiki/Shift-left_testing) which improves developer experience. `check-relative-markdown-links` was built for usage with Lefthook. Here's a minimal example `lefthook.yml` configuration file:

```yml
output:
  - success
  - failure

pre-commit:
  parallel: true
  jobs:
    - name: check-relative-markdown-links
      run: check-relative-markdown-links run
```

### GitHub Actions

This script has been released as a GitHub Action in my [actions monorepo](https://github.com/anttiharju/actions/tree/v0/check-relative-markdown-links). Here's a minimal workflow `.github/workflows/validate.yml` example:

```yml
on:
  push:
    branches:
      - main
  pull_request:

jobs:
  validate:
    runs-on: ubuntu-24.04
    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: check-relative-markdown-links
        uses: anttiharju/actions/check-relative-markdown-links@c90df6253f5cbdd74ac7f483f5b8b192f3b286bf
```
