# Tagging Strategy

## Required Tags
1. **Environment:** production | staging | development
2. **Owner:** team-name or email
3. **Project:** project-identifier  
4. **CostCenter:** department code

## Tag Naming Conventions
- Keys: PascalCase (Environment, Owner)
- Values: lowercase-with-dashes (web-application)

## Enforcement
- AWS Config rule: required-tags
- Applied at resource creation via IaC templates

