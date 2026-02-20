# GitHub Workflow for Terraform deployment

This repository demonstrates how to set up a GitHub repository with Environments and corresponding variables
that are passed through workflows to drive deployment of a multi-configuration-layer Terraform project.

# Prerequisites

* One or more AWS accounts

* GitHub integration application installed in the organisation or repository
  (AWS Connector for GitHub)[https://docs.aws.amazon.com/dtconsole/latest/userguide/connections-create-github.html]
* Terraform remote state S3 bucket per account (see instructions)
* IAM Role for Terraform to assume per account (see instructions)
* CodeBuild project to host GitHub Runner per account (see instructions)

# GitHub Configuration

## Repository variables

| Variable Name | Value | Description |
| - | - | - |
| PROJECT_NAME | MyCoolProject | Short but helpful prefix for resources and tags |
| CONFIG_LAYER_PATH | source/terraform/configuration_layers | Where to find list of config layers in the repo |

## Per-Environment variables

| | dev | stg | prd | Description |
| - | - | - | - | - |
| AWS_REGION | eu-west-2 | eu-west-2 | eu-west-2 | Region for each environment |
| TF_DEPLOY_ROLE_ARN | arn:aws:.... | arn:aws:.... | arn:aws:.... | Runner's role to perform terraform operations |
| TF_STATE_BUCKET_NAME | tfstate-dev-xxxx | tfstate-stg-xxxx | tfstate-prd-xxxx | S3 bucket to hold Terraform state files |

N.B. AWS Account number is derived from the Terraform role ARN to avoid risk of conflicting definitions.