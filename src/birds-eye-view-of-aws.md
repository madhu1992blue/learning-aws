# Bird's eye view of AWS

- AWS: Amazon Web Services is a Cloud offering which contains Network Accessible Services with pay-as-you-go pricing model

## Shared Responsibility Model

Its a security model that defines the security responsibilities of AWS and the customer..

- AWS is responsible for the security of the cloud
  - HW, SW, Networking, Facilities, Regions, AZs, Edge Locations, Storage
- Customer is responsible for security in the cloud
  - Data, Identity, Applications, OS, Network & Firewall Configurations

## AWS Account

- An AWS account:
  - is a container for resources
  - is Unit of billing
  - is where Access control is done using IAM
  - has exactly one root user associated with a unique email address.

## AWS Organization

An AWS Organization helps you manage multiple AWS accounts centrally.

## AWS Resources (ID by ARN)

AWS resources are uniquely and globally identified with Amazon Resource Name (ARN)

```
#ARN Format
arn:<partition>:<service>:<region>:<account-id>:<resource-id>
```

- `arn`: fixed string
- `<partition>`: aws (standard), aws-cn (China), aws-us-gov (GovCloud)
- `<service>`: e.g., s3, ec2, iam
- `<region>`: Optional Region info e.g., us-east-1, us-west-2 . Some services are global and do not require region info
- `<account-id>`: 12 digit AWS account ID
- `<resource-id>`: e.g., instance/i-1234567890abcdef0

## AWS Health Dashboard

- Shows important events that affect your AWS resources.
- It's a global service.
