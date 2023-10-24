# Deployer

A simple Node.js app showing different ways to use secrets in Actions:

- GitHub Secrets in Repo and Environments.
- Using OIDC to avoid storing secrets at all.
- Getting Secrets from Azure Key Vault.

## Workflows

The deploy.yml workflow is the orchestrator, calling the other reusable workflows.:

```mermaid
flowchart LR

A(deploy.yml) -->|Calls| B(build.yml)
B(build.yml) -->|Uploads Artifact| G[Build Artifact]
A(deploy.yml) -->|Calls| C(container-publish.yml)
C(container-publish.yml) -->|Outputs| H[Container Image in ACR]
A(deploy.yml) -->|Calls| D(deploy-with-secrets.yml) -->[Dev Environment]
A(deploy.yml) -->|Calls| E(deploy-with-keyvault.yml) -->[Test Environment]
A(deploy.yml) -->|Calls| F(deploy-with-oidc.yml) -->[Prod Environment]
```
(This is an embedded [Markdown defined Mermaid diagram](https://github.blog/2022-02-14-include-diagrams-markdown-files-mermaid/))

