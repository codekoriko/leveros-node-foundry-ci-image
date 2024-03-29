# CI-CD image for hardhat-foundry

- Needed to run forge & hardhat unittest in CI-CD pipelines.
- Simply merges node:20 and ghcr.io/foundry-rs/foundry:latest.
- It is being rebuilt everyday with the lastest foundry version.

## GitLab usage

```yaml
include:
  - template: Security/SAST.gitlab-ci.yml

variables:
  GIT_SUBMODULE_STRATEGY: recursive

stages:
  - test-forge

sast:
  # You can override the included template(s) by including variable overrides
  # SAST customization: https://docs.gitlab.com/ee/user/application_security/sast/#customizing-the-sast-settings
  # Secret Detection customization: https://docs.gitlab.com/ee/user/application_security/secret_detection/#customizing-settings
  # Dependency Scanning customization: https://docs.gitlab.com/ee/user/application_security/dependency_scanning/#customizing-the-dependency-scanning-settings
  # Container Scanning customization: https://docs.gitlab.com/ee/user/application_security/container_scanning/#customizing-the-container-scanning-settings
  # Note that environment variables can be set in several places
  # See https://docs.gitlab.com/ee/ci/variables/#cicd-variable-precedence
  stage: test-forge

test-forge-job:
  stage: test-forge
  image: ghcr.io/codekoriko/node20-foundry-nightly:latest
  script:
    - npm i
    - forge install
    - forge test -vvv

```
