# .github

[![Lint Code Base](https://github.com/pacroy/.github/actions/workflows/linter.yml/badge.svg)](https://github.com/pacroy/.github/actions/workflows/linter.yml) [![Check Markdown Links](https://github.com/pacroy/.github/actions/workflows/mdlink.yml/badge.svg)](https://github.com/pacroy/.github/actions/workflows/mdlink.yml)

This repository contains common GitHub Actions workflows that you want to run across repositories but you want to maintain them in one place instead of doing it in each repository one by one.

This works by placing all workflow YAML files with minimum lines of codes in the target repositories and they will [reuse the workflows](https://docs.github.com/en/actions/using-workflows/reusing-workflows) in this repository where your most lines of codes are. Sync Files workflow can also be used to automate this process.

Note: This sync process is designed to work well with [GitHub Flow](https://docs.github.com/en/get-started/quickstart/github-flow).

## Common Workflows

- [Lint Code Base](.github/workflows/linter.yml)
- [Check Markdown Links](.github/workflows/mdlink.yml)

## User Guide

### Sync in Automatic Way

To sync all common workflow YAML files to your target repository:

1. In the target repository, create a new workflow file `.github/workflows/sync.yml` with the content from [Sync Files workflow](.github/workflows/sync.yml) workflow.

2. Commit, push, and create a new Pull Request. The Sync Files workflow will run and automatically sync all other workflow files.

3. Push an empty commit as needed to trigger all synced workflows.

### Sync using SSH

If you get an issue pushing changes to your target repository or you prefer to push using SSH key then follow this extra instruction:

1. Make sure you have followed instruction in [Sync in Automatic Way](#sync-in-automatic-way).

2. Create a new SSH key:

    ```sh
    ssh-keygen -t rsa -b 4096 -f id_rsa -N "" -C "your_repository@github.com/your_org"
    ```

    This will generate two files containing private (`id_rsa`) and public key (`id_rsa.pub`).

3. Use command `cat id_rsa.pub` to show the public key.

4. Add public key to the target repository's [Deploy keys](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/managing-deploy-keys#deploy-keys).

5. Use command `cat id_rsa` to show the private key.

6. Create a new secret in the target reposity named `SYNC_SSH_KEY` with private key as the value.

7. Trigger the workflow.

8. Once everything is working, you may remove both SSK key files.

### Sync in Manual Way

1. Copy all [common workflow files](#common-workflows) to folder `.github/workflows` in the target repository.

2. Commit and push to trigger all workflows.

### Customize Linters

You can customize linters in each target repository by setting additional environment variables according to the [linter documentation](https://github.com/super-linter/super-linter/blob/main/README.md). An environment variable can be set by creating a file named `ENVIRONMENT_NAME.var` in the folder `.github/linters` within your target repository.

For example, if you want to disable KUBECONFORM linter, create file `VALIDATE_KUBERNETES_KUBECONFORM.var` with value `false` as the content. Put the file in the folder `.github/linters` within your target repository. All variables files will be automatically loaded and used by the linters.

## Maintainer Guide

To get the workflows run with latest codes from your branches:

1. Create branch and make changes.

2. Force update and push tag first.

    ```sh
    git tag -am "v1" v1 --force
    git push origin v1 --force
    ```

3. Commit and push the changes.
