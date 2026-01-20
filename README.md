# Lab M7.02 - Implementing Cost Allocation Tags

**Repository:** [https://github.com/cloud-engineering-bootcamp/ce-lab-implementing-cost-allocation-tags](https://github.com/cloud-engineering-bootcamp/ce-lab-implementing-cost-allocation-tags)

**Activity Type:** Individual  
**Estimated Time:** 45-60 minutes

## Learning Objectives

- [ ] Design a tag taxonomy for cost tracking
- [ ] Apply tags to AWS resources
- [ ] Activate cost allocation tags
- [ ] View costs by tags in Cost Explorer
- [ ] Enforce tagging with AWS Config

## Prerequisites

- [ ] AWS account with resources running
- [ ] IAM permissions to tag resources and manage Cost Allocation Tags
- [ ] Completed Module 7 Lessons 1-3

## Introduction

Tags are the foundation of cost visibility. Without them, you can't track costs by team, project, or environment.

## Scenario

Your organization has 50+ AWS resources but no tagging strategy. The finance team can't attribute costs to teams. Your task: implement cost allocation tags.

## Your Task

1. Design tag taxonomy (4-6 required tags)
2. Tag at least 10 existing resources
3. Activate cost allocation tags
4. Create Cost Explorer view by tags
5. Document tagging strategy

**Time limit:** 45-60 minutes

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

## Submission

GitHub repository with:
1. `tagging-strategy.md`
2. `tag-compliance-report.md`
3. Screenshots (costs by tags, Config compliance)
4. `README.md`

## Verification Checklist

- [ ] Designed tag taxonomy (4-6 tags)
- [ ] Tagged at least 10 resources
- [ ] Activated cost allocation tags
- [ ] Created Cost Explorer view by tags (after 24hrs)
- [ ] Set up AWS Config rule for required tags
- [ ] Documented strategy and compliance
- [ ] All files in GitHub

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

## Additional Resources

- [Tagging Best Practices](https://docs.aws.amazon.com/whitepapers/latest/tagging-best-practices/tagging-best-practices.html)

**Good luck! 🚀**
