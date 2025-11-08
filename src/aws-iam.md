# AWS Identity and Access Management (IAM)

- One root user per account.
- Root user has full access to all resources in the account.
- Email address is used as the username for root user.

## Best Practices for Root User

### Use DL (Distribution List) email address
- Don't use one users email address as it could send important communication like billing alerts or resource security notifications to that email.
- Instead, use a distribution list email address that multiple people in your org can access.

### Enable Multi-Factor Authentication (MFA)
- Adds an extra layer of security to your root user account.

### Disable API Token Access

- Prevents programmatic access to your root user account. Root is only needed for a few tasks.
- Create an IAM user with admin privileges for day-to-day tasks instead of using root user.

## Certain Tasks that can only be performed by Root User
- Changing account settings
- Closing the AWS account
- Restoring IAM user permissions
- Configuring MFA delete on S3 buckets
- Edit S3 Bucket policy with invalid VPC ID or VPC endpoint ID
- Signing up for GovCloud
