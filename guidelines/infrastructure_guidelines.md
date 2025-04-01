# Infrastructure as Code (IaC)

## Introduction

Infrastructure as Code (IaC) is the process of managing and provisioning computing infrastructure through machine-readable definition files rather than manual hardware configuration or interactive configuration tools. At Smartphonekey, we use IaC to automate our infrastructure deployment, ensuring consistency, repeatability, and reliability across all environments.

## Tools We Use

At Smartphonekey, we use the following tools for implementing Infrastructure as Code:

- **Terraform**: Our primary IaC tool for defining and provisioning infrastructure
- **GitLab CI/CD**: For automating our infrastructure deployment pipelines
- **Google Cloud Platform (GCE)**: Our primary cloud provider
- **Supabase**: For managed PostgreSQL database services
- **GitHub Actions**: For CI/CD in GitHub-hosted projects

## Core Principles

### Declarative Over Imperative

We prefer declarative infrastructure definitions that specify the desired end-state rather than the steps to get there. This approach allows Terraform to determine the optimal way to reach the desired state.

### Version Control Everything

All infrastructure code is stored in version control (GitLab), providing:
- Change history
- Collaboration through merge requests
- Code reviews for infrastructure changes
- Rollback capabilities

### Infrastructure as Cattle, Not Pets

We treat infrastructure as replaceable units rather than unique, irreplaceable systems. This enables us to:
- Quickly recreate environments
- Test infrastructure changes safely
- Implement disaster recovery more effectively

### Automation Over Manual Operations

We automate infrastructure operations whenever possible to:
- Reduce human error
- Ensure consistency
- Improve deployment speed
- Focus human resources on higher-value activities

## Terraform Best Practices

### Project Structure

We organize our Terraform code following this structure:

```
terraform/
├── environments/
│   ├── production/
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   ├── outputs.tf
│   │   └── terraform.tfvars
│   ├── staging/
│   └── development/
├── modules/
│   ├── network/
│   ├── database/
│   ├── compute/
│   └── storage/
└── scripts/
    └── apply-terraform.sh
```

### Module Usage

- Create reusable modules for common infrastructure patterns
- Keep modules focused on specific concerns
- Document modules with README files and variable descriptions
- Version modules to maintain backward compatibility

### State Management

- Use GitLab-managed Terraform state or Google Cloud Storage buckets for state files
- Enable state locking to prevent concurrent modifications
- Separate state by environment to reduce risk
- Restrict access to state files as they may contain sensitive information

### Security Practices

- Use GitLab or GitHub secrets for storing sensitive values
- Implement least privilege access for service accounts
- Scan infrastructure code for security issues using tools like tfsec or Checkov
- Apply resource policies to enforce security standards

## GitLab CI/CD Pipeline for Terraform

We use the following GitLab CI/CD pipeline structure for Terraform:

```yaml
stages:
  - validate
  - plan
  - apply

variables:
  TF_ROOT: ${CI_PROJECT_DIR}/terraform
  TF_STATE_NAME: ${CI_PROJECT_NAME}-${CI_ENVIRONMENT_NAME}

cache:
  key: ${CI_COMMIT_REF_SLUG}
  paths:
    - ${TF_ROOT}/.terraform

validate:
  stage: validate
  script:
    - cd ${TF_ROOT}
    - terraform init -backend-config="key=${TF_STATE_NAME}"
    - terraform validate
    - terraform fmt -check
  rules:
    - if: '$CI_PIPELINE_SOURCE == "merge_request_event"'

plan:
  stage: plan
  script:
    - cd ${TF_ROOT}
    - terraform init -backend-config="key=${TF_STATE_NAME}"
    - terraform plan -out=plan.tfplan
  artifacts:
    paths:
      - ${TF_ROOT}/plan.tfplan
  rules:
    - if: '$CI_PIPELINE_SOURCE == "merge_request_event"'

apply:
  stage: apply
  script:
    - cd ${TF_ROOT}
    - terraform init -backend-config="key=${TF_STATE_NAME}"
    - terraform apply -auto-approve
  environment:
    name: $CI_ENVIRONMENT_NAME
  rules:
    - if: '$CI_COMMIT_BRANCH == "main" && $CI_ENVIRONMENT_NAME'
      when: manual
```

## Supabase Integration with Terraform

### Setting Up Supabase with Terraform

1. Define your Supabase resources using Terraform
2. Manage database migrations through code
3. Set up appropriate security policies using Row Level Security (RLS)
4. Configure authentication and authorization

Example Terraform configuration for Supabase:

```hcl
# Example Supabase project configuration
resource "supabase_project" "example" {
  name        = "smartphonekey-${var.environment}"
  db_password = var.db_password
  region      = "us-west-2"
}

# Database schema
resource "supabase_database" "example" {
  project_id = supabase_project.example.id
  
  # Migration script
  migration_file = "${path.module}/migrations/initial.sql"
}

# Authentication settings
resource "supabase_auth_settings" "example" {
  project_id = supabase_project.example.id
  
  disable_signup = false
  jwt_expiry     = 3600
}
```

## Continuous Deployment Workflow

We implement a GitOps workflow where:

1. Infrastructure changes are proposed through merge/pull requests
2. The CI/CD pipeline validates changes and generates a plan
3. Team members review the proposed changes
4. Changes are applied automatically to development environments and manually to production

### Benefits

- Consistent change process across all environments
- Reduced risk through review and approval process
- Visibility into infrastructure changes
- Audit trail for compliance purposes

## Monitoring and Drift Detection

We regularly check for configuration drift to ensure our actual infrastructure matches our defined code:

- Schedule regular drift detection jobs
- Alert on unauthorized changes
- Remediate drift by reapplying Terraform configurations
- Document exceptions when manual changes are required

## Best Practices for AI Agent Interaction

When AI agents assist with infrastructure code, follow these guidelines:

### For AI Agents

- Check for existing modules before creating new ones
- Follow established naming conventions and code structure
- Look for common patterns in how resources are configured
- Consider security implications of suggested changes
- Include appropriate documentation for any generated code

### For Developers Working with AI Agents

- Provide context about the infrastructure architecture
- Specify which modules should be reused
- Review AI-generated infrastructure code carefully before applying
- Ensure generated code follows security best practices

## Troubleshooting

Common issues when working with our infrastructure code:

1. **State Lock Issues**
   - Check if another pipeline is running
   - Use `terraform force-unlock` if a lock is stale

2. **Authentication Failures**
   - Verify service account permissions
   - Check credential expiration
   - Ensure environment variables are properly set

3. **Resource Conflicts**
   - Use `terraform import` to bring manually created resources under Terraform management
   - Check for resources managed by multiple Terraform configurations

## Conclusion

Infrastructure as Code is a foundational practice at Smartphonekey that enables us to manage our infrastructure efficiently, consistently, and securely. By following these guidelines and best practices, we ensure that our infrastructure remains reliable, scalable, and well-documented for both human and AI operators.