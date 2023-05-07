# .github

This repository contains common GitHub Actions workflows that you want to run across repositories but you want to maintain them in one place instead of doing it in each repository one by one.

This works by placing all workflow YAML files with minimum lines of codes in the target repositories and they will [reuse the workflows](https://docs.github.com/en/actions/using-workflows/reusing-workflows) in this repository where your most lines of codes are. [Sync Files](.github/workflows/sync.yml) can also be used to automate this process.

Note: This sync process is designed to work well with [GitHub Flow](https://docs.github.com/en/get-started/quickstart/github-flow).

## Common Workflows

- [Lint Code Base](.github/workflows/linter.yml)
- [Check Markdown Links](.github/workflows/mdlink.yml)
