# Lab M7.02 - Implementing Cost Allocation Tags

**Repository:** https://github.com/MaryaAhmadi/ce-lab-implementing-cost-allocation-tags.git


**Activity Type:** Individual  
**Estimated Time:** 45-60 minutes


##Overview

This lab demonstrates how to implement a cost allocation tagging strategy in AWS to improve cost visibility, accountability, and governance.
By applying consistent tags across resources and enabling cost allocation tracking, organizations can accurately attribute cloud spending to teams, projects, and environments.


## Learning Objectives

- [ ✅ ] Design a tag taxonomy for cost tracking
- [ ✅ ] Apply tags to AWS resources
- [ ✅ ] Activate cost allocation tags
- [ ✅ ] View costs by tags in Cost Explorer
- [ ✅ ] Enforce tagging with AWS Config

## Prerequisites

- AWS account with active resources (EC2, S3, RDS)
- IAM permissions:
  - tag:TagResources
  - ec2:CreateTags
  - Billing and Cost Management access
- Completion of Module 7 Lessons 1–3




## Scenario
The organization currently operates 50+ AWS resources without a tagging strategy. As a result, the finance team cannot track or allocate cloud costs effectively.

Your task is to implement a tagging strategy that ensures every resource is 
traceable by:
- Environment
- Owner
- Project
- Cost Center

## Implementation Summary
In this lab, the following were completed:

- Designed a tagging strategy (tagging-strategy.md)
- Tagged 10+ AWS resources
- Activated cost allocation tags in Billing Console
- Configured AWS Config rule (required-tags)
- Verified compliance status
- Documented results (tag-compliance-report.md)

## Tagging Strategy

The following tags were defined as mandatory:

TagKey	  | Description

Environment	| Defines deployment environment (development, staging, production)
Owner	   | Responsible team or individual
Project.    | 	Associated project name
CostCenter	|  Department or billing unit

##  Naming Conventions
- Keys: PascalCase (e.g., Environment)
- Values: lowercase-with-dashes (e.g., web-app)

##  Steps Performed

1. Tagging Resources
- Used AWS Tag Editor to apply tags across multiple services
- Tagged at least 10 resources (EC2, S3, RDS)
- Verified tags via resource details and filtering

2. Activating Cost Allocation Tags
- Enabled tags in Billing Console
- Activated:
   - Environment
   - Owner
   - Project
   - CostCenter

⏳ Note: Tags appear in Cost Explorer after ~24 hours

3. Cost Analysis (Pending 24h)
- Cost Explorer configured to group by:
- Environment
- Owner

## 📸 Screenshots:
costs-by-environment.png
costs-by-owner.png

4. AWS Config Rule
- Created rule: required-tags
- Configured required keys:
  - Environment
  - Owner
  - Project
  - CostCenter
- Evaluated compliance across resources

## 📸 Screenshot:
config-compliance.png

## Results
- Successfully tagged all target resources
- Activated cost allocation tags
- AWS Config identified compliant and non-compliant resources
- Governance mechanism implemented for ongoing compliance

## Challenges & Observations
- AWS Config is case-sensitive for tag keys
- Incorrect rule parameters can result in false non-compliance
- Cost Explorer requires time delay after activation
- Some existing resources may initially appear non-compliant


## Step-by-Step Instructions

### Step 1: Design Tag Taxonomy

Create `tagging-strategy.md`:

```markdown
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
```

### Step 2: Tag Existing Resources

**Using AWS Tag Editor:**

1. AWS Console → Resource Groups → Tag Editor
2. Find resources:
   - Region: All regions
   - Resource types: EC2 instance, S3 bucket, RDS database
3. Search
4. Select resources (at least 10)
5. Manage tags → Add:
   - Environment: development (or appropriate value)
   - Owner: your-name
   - Project: bootcamp
   - CostCenter: training

6. Review and apply tags

**Using AWS CLI (alternative):**
```bash
# Tag an EC2 instance
aws ec2 create-tags \
  --resources i-1234567890abcdef0 \
  --tags Key=Environment,Value=development \
         Key=Owner,Value=platform-team \
         Key=Project,Value=web-app \
         Key=CostCenter,Value=eng-001
```

### Step 3: Activate Cost Allocation Tags

1. Billing Console → Cost Allocation Tags
2. Find your tags in "User-defined cost allocation tags"
3. Select: Environment, Owner, Project, CostCenter
4. Click "Activate"
5. **Note:** Takes 24 hours to appear in Cost Explorer

### Step 4: (24 hours later) View Costs by Tags

After 24 hours:

1. Cost Explorer
2. Group by: Tag → Environment
3. View production vs development vs staging costs
4. Take screenshot: `costs-by-environment.png`

5. Create another view:
   - Group by: Tag → Owner
   - See costs per team
   - Screenshot: `costs-by-owner.png`

### Step 5: Set Up AWS Config Rule

Create Config rule for required tags:

1. AWS Config → Rules → Add rule
2. Search "required-tags"
3. Configure:
   - tag1Key: Environment
   - tag2Key: Owner
   - tag3Key: Project  
   - tag4Key: CostCenter
4. Choose resource types: EC2, S3, RDS
5. Create rule

6. Wait for evaluation (5-10 minutes)
7. View compliance: Take screenshot `config-compliance.png`

### Step 6: Document Compliance

Create `tag-compliance-report.md`:

```markdown
# Tag Compliance Report

## Summary
- **Total Resources:** X
- **Tagged Resources:** Y
- **Compliance Rate:** Z%

## Non-Compliant Resources
[List resource IDs and missing tags]

## Remediation Plan
1. Tag remaining resources by [date]
2. Enable tag policies in AWS Organizations
3. Implement IaC tagging defaults

## Screenshots
- costs-by-environment.png
- costs-by-owner.png
- config-compliance.png
```


## Verification Checklist

- [ ✅] Designed tag taxonomy (4-6 tags)
- [ ✅] Tagged at least 10 resources
- [ ✅] Activated cost allocation tags
- [ ✅] Created Cost Explorer view by tags (after 24hrs)
- [ ✅] Set up AWS Config rule for required tags
- [ ✅] Documented strategy and compliance
- [ ✅] All files in GitHub

## Troubleshooting

**Tags not appearing in Cost Explorer:**
- Wait 24 hours after activation
- Check tags are activated in Cost Allocation Tags
- Resources must be tagged after activation date

**Can't tag resources:**
- Check IAM permissions
- Some resources require specific permissions

**Config rule shows non-compliant:**
- Expected for existing resources
- Remediate by adding missing tags
- Prevent with tag policies


## Conclusion
This lab demonstrates how proper tagging improves:
- Cost visibility
- Accountability
- Governance
By combining tagging strategies with AWS Config enforcement, organizations can maintain consistent and reliable cloud cost tracking.

## Additional Resources

- [Tagging Best Practices](https://docs.aws.amazon.com/whitepapers/latest/tagging-best-practices/tagging-best-practices.html)

**Good luck! 🚀**
