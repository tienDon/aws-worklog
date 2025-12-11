---
title: "Blog 4"
date: "2025-12-09"
weight: 1
chapter: false
pre: " <b> 3.4. </b> "
---

# Choosing the Right Execution Options for Your SaaS Product in the AWS Marketplace

**Author:**

Pawan Kumar, Technical Account Manager at Amazon Web Services

_Date: March 28, 2025_

<style>
body {
font-family: "Times New Roman", Times, serif;

font-size: 13px;

}

h1 {
font-size: 24px;

}

h2 {
font-size: 18px;

}

h3 {
font-size: 16px;

}
</style>

[AWS Marketplace](https://aws.amazon.com/marketplace/) sellers, independent software vendors (ISVs), and consulting partners (CPs) need to provide execution options when launching software-as-a-service (SaaS) products in the AWS Marketplace. Choosing the right execution option is crucial. This choice affects how customers access your product and can truly impact their experience. Let's explore the available execution options to help you make an informed choice for your SaaS service.

## Prerequisites

Before you choose an execution option, you must register as an AWS Marketplace seller. For more information, see [Registering as an AWS Marketplace seller](https://docs.aws.amazon.com/marketplace/latest/userguide/seller-registration-process.html) in the AWS Marketplace Seller Guide.

## Execution Options

AWS Marketplace allows you to choose from two execution options when listing a SaaS product. The execution option defines the experience your customers have after registering your product in AWS Marketplace.

1. **Default Execution URL:** This option allows you to design and manage the entire onboarding experience. It works well for SaaS products that don't require additional resources in the customer's AWS account. The key details are:

• Customers are redirected to your product registration page after signing up.

• You, as the vendor, control the entire registration experience and provide customers with the steps to access the product.

2. **SaaS Quick Launch:** This option works well if your SaaS product requires AWS resources deployed in the customer's account. For example, vendors who deploy [AWS Identity and Access Management roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles.html), databases, or agents in the customer's AWS account can simplify the onboarding experience for their customers. Key details are:

• SaaS Quick Launch uses integrations to create the [AWS CloudFormation](https://aws.amazon.com/cloudformation/) stack to deploy resources with fewer context switches for customers.

• Deployment secrets can be stored in the customer's [AWS Secrets Manager](https://aws.amazon.com/secrets-manager/) and used by AWS CloudFormation during deployment. This avoids the need for customers to copy and paste deployment parameters.

• It provides step-by-step guidance including integrated authorization verification mechanisms to ensure customers have the necessary AWS credentials.

• Products with SaaS Quick Launch display a Quick Launch tag in their descriptions.

For more information, see [Enabling SaaS Quick Launch](https://catalog.workshops.aws/mpseller/en-US/saas/quick-launch-integration).

## Conclusion and Next Steps

In this post, we covered two execution options available for SaaS products in the AWS Marketplace. After choosing the execution option that best suits your needs, you can proceed with listing your SaaS in the AWS Marketplace. You may find the following resources helpful once you begin the listing process.

• [Practice Exercise: Creating a SaaS Listing](https://catalog.workshops.aws/mpseller/en-US/saas/create-listing)

• [Practice Exercise: Integrating Your SaaS](https://catalog.workshops.aws/mpseller/en-US/saas/integration)

• [Practice Exercise: Enabling SaaS Quick Launch](https://catalog.workshops.aws/mpseller/en-US/saas/quick-launch-integration)

• [Successfully Testing Your SaaS Listing in AWS Marketplace](https://aws.amazon.com/blogs/awsmarketplace/successfully-testing-your-saas-listing-in-aws-marketplace/)

• [Update Product Visibility] [product](https://docs.aws.amazon.com/marketplace/latest/userguide/saas-product-settings.html#saas-update-visibility)

## About the Author

Pawan Kumar is a Technical Account Manager at Amazon Web Services, specializing in AWS Marketplace solutions and serverless architecture. He develops innovative strategies to address complex customer challenges. He aims to drive cloud adoption across industries. Outside of work, Pawan enjoys playing cricket and following international tournaments.

**TAGS:** [AWS Marketplace](https://aws.amazon.com/blogs/awsmarketplace/category/software/aws-marketplace/), [Best Practices](https://aws.amazon.com/blogs/awsmarketplace/category/post-types/best-practices/), [Foundational (100)](https://aws.amazon.com/blogs/awsmarketplace/category/learning-levels/foundational-100/), [SaaS](https://aws.amazon.com/blogs/awsmarketplace/category/saas/), [Software](https://aws.amazon.com/blogs/awsmarketplace/category/software/)
