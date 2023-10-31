# Helm Chart Publishing

Publish Helm Charts.

## Layout

Top level directory names serve as the name of the helm repository to push into:

```text
└── <helm_chart>
    └── Chart.yaml...
```

Each subdirectory to publish includes a valid Helm chart.

## Dependency and Documentation Update

### Secrets and Deploy Key

Create a deployment key and load it as a GitHub action secret using `bin/load_deploy_key` script.

### SSH_DEPLOY_PRIVATE_KEY Secret

If the SSH_DEPLOY_PRIVATE_KEY is created for the GitHub action and the corresponding public key is added
as a deployment key with write privileges, Helm dependencies and documentatin is created and updated
to the default branch on PR merge.

## Labels

### Do Not Merge

A `Do Not Merge` label prevents a PR from being merged using the `do_not_merge.yml` [workflow](.github/workflows/do_not_merge.yml)

### Versioning

Tags are in \<repository>/v\<version> format, set by the `version` in the Helm chart `Chart.yaml` file.

## Pre-Commit

Install `pre-commit`:

- using brew: `brew install pre-commit`

The pre-commit requires local binaries for `actionlint` and `shellcheck`.

`brew install actionlint shellcheck`

Install the `.pre-commit-config.yaml` definition to your repository copy:

`pre-commit install`

Run pre-commit on all files, regardless of commit or status:

`pre-commit run --all-files`

### Helm Docs

[Helm docs](https://github.com/norwoodj/helm-docs) pre-commit automatically updates Helm chart documentation.

Update `.helmdocsignore` to include any directories to not publish docs for, i.e. `bin` or other support directories.
