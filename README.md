# Deployer

A simple Node.js app to use as an example for workflows using GitHub Actions.

## Workflow status
[![.github/workflows/deploy_prod.yml](https://github.com/gidavies/SimpleWebApp/actions/workflows/deploy_prod.yml/badge.svg)](https://github.com/gidavies/SimpleWebApp/actions/workflows/deploy_prod.yml)

[![.github/workflows/deploy_test.yml](https://github.com/gidavies/SimpleWebApp/actions/workflows/deploy_test.yml/badge.svg)](https://github.com/gidavies/SimpleWebApp/actions/workflows/deploy_test.yml)

[![.github/workflows/pr_checks.yml](https://github.com/gidavies/SimpleWebApp/actions/workflows/pr_checks.yml/badge.svg)](https://github.com/gidavies/SimpleWebApp/actions/workflows/pr_checks.yml)

## Workflows

The Node app can be deployed to Azure App Service with the included workflows, which are based on the default Actions. There are workflows that are triggered on the following events:
- Creating a PR.
- Adding a label during a PR.
- Merging into main.

There are two reusable workflows:
- build.yml which performs an npm install, build and test,
- deploy_to_azure.yml which deploys the web app to Azure App Service.

These are called by three calling workflows:

```mermaid
flowchart LR

A(PR) -->|Triggers| B(pr_checks.yml)
B -->|Calls| C(build.yml)
D(Add label in PR) -->|Triggers| E(deploy_test.yml)
E -->|Calls| C(build.yml)
E -->|Calls| F(deploy_to_azure.yml)
G(Push to main) -->|Triggers| H(deploy_prod.yml)
H -->|Calls| C(build.yml)
H -->|Calls| F(deploy_to_azure.yml)
F -->|Needs| C(build.yml)
```
(This is an embedded [Markdown defined Mermaid diagram](https://github.blog/2022-02-14-include-diagrams-markdown-files-mermaid/))

