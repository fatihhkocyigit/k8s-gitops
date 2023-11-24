# k8s-gitops
Kubernetes GitOps example with IaC approach.
This repository includes;
- IaC approach for EKS Kubernetes cluster creation with AWS best practices
- CI/CD with GitOps practices
- Secret management in K8s cluster with AWS Secret Manager
- Monitoring tools, such as Cloudwatch, Grafana, Prometheus

# Terraform Repository

Terraform Repository For k8s-gitops Terraform Infrastructure.

## Scope

The purpose of the project is to create a re-usable AWS infrastructure with an IaC approach using Terraform and Terragrunt. It is important to understand the fundamentals and milestones of Terraform and Terragrunt to understand this project.

- [Terraform Docs](https://www.terraform.io/docs)
- [Terragrunt Docs](https://terragrunt.gruntwork.io/docs/)


### Pre-requisites

1. Install [Terraform](https://www.terraform.io/) version `1.2.0` or newer and
   [Terragrunt](https://github.com/gruntwork-io/terragrunt) version `v0.38.0` or newer.
2. Configure your AWS credentials using one of the supported [authentication
   mechanisms](https://www.terraform.io/docs/providers/aws/#authentication).  The account you configured must have permission to assume a role on the account that will be used for Terraform operations.
3. Fill in your AWS Account IDs in `<`environment>/<country>/account.hcl` which will be assumed for the terraform operations.


## Folder Structure

The code in this repo uses the following folder hierarchy:

```
root
 └ _envcommon
 └ environment
    └ env.hcl
    └ country/group
        └ account.hcl
        └ region
            └ region.hcl
            └ resource
        
```

Where:

* **Root Level**: At the top level are each of your Folders, such as `stage`, `prod`, `dev`,
  etc. There is also a `_`envcommon` folder
  that defines resources that are available across all the environments for all continents.
* **Environment**: Within each environment, you can deploy all the resources for that environment. There is a `env.hcl` file that defines environment-level variables.
* **Resource**: Within each Resource, you can deploy the specific resource for that AWS Region.
  
## How do you deploy the infrastructure in this repo?

### Deploying a single module for resources

1. `cd` into the module's folder (e.g. `cd platform/vpc`).
2. Run `terragrunt plan` to see the changes you're about to apply.
3. If the plan looks good, run `terragrunt apply`.

### Deploying all modules in a region

1. `cd` into the region folder (e.g. `cd platform`).
2. Run `terragrunt run-all plan` to see all the changes you're about to apply.
3. If the plan looks good, run `terragrunt run-all apply`.

### Deploying all modules in a country

1. `cd` into the region folder (e.g. `cd platform`).
3. Configure your OpsGenie-Promotheus integration API key:`export TF_VAR_prometheus_stack_alertmanager_opsgenie_api_key=(...)`.
4. Configure your OpsGenie-AWS CloudWatch integration API key:`export OPSGENIE_AWS_CLOUDWATCH_API_KEY=(...)`.
5. Run `terragrunt run-all plan` to see all the changes you're about to apply.
6. If the plan looks good, run `terragrunt run-all apply`.

### Deploying all modules in an environment

1. `cd` into the region folder (e.g. `cd platform`).
3. Run `terragrunt run-all plan` to see all the changes you're about to apply.
4. If the plan looks good, run `terragrunt run-all apply`.

