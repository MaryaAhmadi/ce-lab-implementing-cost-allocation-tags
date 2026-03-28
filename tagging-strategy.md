# Tagging Strategy

## Purpose
This tagging strategy ensures AWS costs can be tracked by environment, owner, project, and cost center.

## Required Tags
1. **Environment:** production | staging | development
2. **Owner:** team-name or email
3. **Project:** project-identifier
4. **CostCenter:** department code
5. **ManagedBy:** terraform | cloudformation | manual

## Tag Naming Conventions
- Keys use PascalCase: `Environment`, `Owner`, `Project`, `CostCenter`, `ManagedBy`
- Values use lowercase-with-dashes: `platform-team`, `web-app`, `eng-001`
- Avoid spaces in values
- Use consistent project names across all resources

## Example
- Environment: development
- Owner: your-name
- Project: bootcamp
- CostCenter: training
- ManagedBy: manual

## Enforcement
- AWS Config rule: `required-tags`
- Tags applied at resource creation via IaC templates
- Existing resources remediated using AWS Tag Editor or CLI

## Scope
This strategy applies to:
- EC2 instances
- S3 buckets
- RDS databases
- Other supported AWS resources
