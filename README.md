# Renovate-Global-Configuration

Global Renovate Configuration for Hapag-Lloyd repositories.

## Default Configuration

- discover all projects except forks
- use semantic commits
- ignore Terraform provider definitions in local modules
- flag all PRs with `dependency`
- try to auto-merge where possible (for patches and minor updates)
- update AWS packages on mondays before noon only due to high frequency of updates
- update all Repology packages in one PR. Especially useful for Alpine as all packages have to be updated at once.

## Version Updates in Dockerfiles

```dockerfile
# renovate: datasource=repology depName=alpine3.17/curl
ENV CURL_VERSION="1.2.3"

RUN apk add --no-cache curl=${CURL_VERSION}
```