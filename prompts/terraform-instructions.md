# Copilot Code Generation Instructions for Azure Terraform

This document defines the standards and best practices to follow when generating Terraform code for Azure resources.

## General Guidelines

- Use Terraform best practices for Azure resource deployment
- Use Azure Verified Modules (AVM) whereever possible
- Follow a consistent naming convention for resources
- Organize resources by modules for better maintainability
- Always include appropriate tagging for all resources
- Use variables for configurable values where applicable
- Include descriptive comments for complex resource configurations

## Naming Conventions

- Use snake_case for all resource names, variables, and outputs
- Follow the pattern: `{prefix}-{resource_type}-{purpose}-{environment}`
- Keep names concise but descriptive

## Resource Organization

- Group related resources into modules
- Structure modules with:
    - `main.tf` - Core resource definitions
    - `variables.tf` - Input variables
    - `outputs.tf` - Module outputs
    - `README.md` - Module documentation

## Security Practices

- Never hardcode secrets or credentials
- Use Azure Key Vault for sensitive information
- Implement proper IAM permissions using role assignments
- Enable diagnostic settings for auditing, but have it commented out to save on cost
- Follow the principle of least privilege

## Performance and Cost Optimization

- Use appropriate SKUs based on workload requirements
- Implement auto-scaling where appropriate
- Configure lifecycle rules to prevent accidental resource deletion
- Use tags for cost allocation and tracking
- Disabled Availability Zones for all resources to save on cost.
- Use Azure LRS Storage Accounts for cost efficiency

## Testing and Validation

- Include validation rules for input variables
- Use `terraform validate` and `terraform plan` before applying changes
- Implement automated testing for infrastructure code

## Example Structure

```terraform
# main.tf
resource "azurerm_resource_group" "example" {
    name     = "rg-play-lscph-example"
    location = var.location
    
    tags = {
        Environment = var.environment
        Project     = var.project_name
        ManagedBy   = "Terraform"
    }
}
