# .github

[![Lint Code Base](https://github.com/pacroy/.github/actions/workflows/linter.yml/badge.svg)](https://github.com/pacroy/.github/actions/workflows/linter.yml) [![Check Markdown Links](https://github.com/pacroy/.github/actions/workflows/mdlink.yml/badge.svg)](https://github.com/pacroy/.github/actions/workflows/mdlink.yml)

This repository contains common GitHub Actions workflows that you want to run across repositories but you want to maintain them in one place instead of doing it in each repository one by one.

This works by placing all workflow YAML files with minimum lines of codes in the target repositories and they will [reuse the workflows](https://docs.github.com/en/actions/using-workflows/reusing-workflows) in this repository where your most lines of codes are. Sync Files workflow can also be used to automate this process.

Note: This sync process is designed to work well with [GitHub Flow](https://docs.github.com/en/get-started/quickstart/github-flow).

## Common Workflows

- [Lint Code Base](.github/workflows/linter.yml)
- [Check Markdown Links](.github/workflows/mdlink.yml)

## User Guide

### Automatic Way

1. In target repository, create a new workflow file `.github/workflows/sync.yml` with the content from [Sync Files workflow](.github/workflows/sync.yml) workflow.

2. Commit, push, and create a new Pull Request. The Sync Files workflow will run and automatically sync all other workflow files.

3. Push an empty commit as needed to trigger all synced workflows.

### Manual Way

1. Copy all [common workflow files](#common-workflows) to folder `.github/workflows` in your target repository.

2. Commit and push to trigger all workflows.
