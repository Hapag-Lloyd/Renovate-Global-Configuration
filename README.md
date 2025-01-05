# Renovate-Global-Configuration

This repository contains the global configuration settings useful for all Hapag-Lloyd repositories. Renovate is
scheduled to run every 6 hours on all repositories we have.

## Usage

Make sure to include the default configuration in your `renovate.json` file.

```json
{
  "extends": ["github>Hapag-Lloyd/Renovate-Global-Configuration"]
}
```

## Default Configuration

- discover all projects except forks
- use semantic commits
- ignore Terraform provider definitions in local modules
- flag all PRs with `dependency`
- try to auto-merge where possible (for patches and minor updates)
- update AWS packages on monday morning only due to high frequency of updates
- update all Repology packages in one PR. Especially useful for Alpine as all packages have to be updated at once.
- allow updates of AMI images
- update dependant project workflows on the 1st of every month to reduce the number of PRs

## Special Version Updates

Supported files: `Dockerfile*`, `terraform.yml`, `tflint.hcl`.

```dockerfile
# renovate: datasource=repology depName=alpine3.17/curl
ENV CURL_VERSION="1.2.3"

RUN apk add --no-cache curl=${CURL_VERSION}
```

```shell
# renovate: datasource=github-tags depName=terraform-linters/tflint
abc_version="1.2.3"
curl -o a.tgz https://my.dependency?${abc_version}
```

```hcl
plugin "aws" {
  # renovate: datasource=github-tags depName=terraform-linters/tflint
  version = "1.2.3"
}
```

```hcl
# renovate: amiFilter=[{"Name":"owner-id","Values":["137112412989"]},{"Name":"name","Values":["amzn2-ami-hvm-*-x86_64-ebs"]}]
# currentImageName=ami-0dffacdad8c0f8540
default_ami_id = "ami-0dffacdad8c0f8540"
```
