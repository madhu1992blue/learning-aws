# IAM Service

- Enables Authentication(AuthN) and Authorization(AuthZ) for AWS services and resources.
  - AuthN: Verifying the identity of a user or service trying to access AWS resources.
  - AuthZ: Determining what actions that user or service is allowed to perform on those resources.
- Primarily Designed around Idenity Based Access Control model
- Allows Cross Account Access

### IAM Users

- *IAM User* is a principal Idenity that represents a person or service that interacts with AWS resources.
- IAM Users are allowed to be associated with *permissions(group, inline and managed permissions)*.
- IAM users can be associated with a *permission boundary*.
- IAM user is also a *container for credentials*
  - Sign In Credentials.
  - Access Keys
  - CodeCommit Credentials
  - KeySpaces Credentials

## IAM Groups (No nesting)

- A collection of IAM users.
- Used to manage permissions for multiple users.
- Permissions assigned to a group are inherited by all users in that group.
- Users can be members of multiple groups.
- Groups cannot be nested.

## AWS Policy Types

There are 3 types:
- Permission Policy: Grant permissions to perform actions
  - Identity Based Policy: Policy associated with Identities
  - Resource Based Policy: Policy associated with Resources
  - Session Policy: Policy associated with temporary sessions

- Permission Boundary: Define the maximum permissions that a particular resource can have.
  - IAM Permission Boundaries
  - AWS Organizations Service Control Policies (SCPs)

### Policy Overlap Outcomes

- Identity Based Policies and Resource Based Policies: Union of both policies.
- Identity Policy and Permission Boundaries: Intersection of both policies.

### Permission Evaluation for Policies

#### Evaluation Logic 1: Evaluate Permission Policies

1. AWS has default Deny for all actions.
1. Evaluate all Applicable Permission Policies: The Idenity Based Policies, Resource Based Policies, Session Policies.
1. If there is an explicit deny in any policy, the final result is Deny.
1. If there is no explicit deny, then it goes to Next Step. (Evaluation Logic 2)

#### Evaluation Logic 2: Related to Organization with an SCPs (Service control Policy)

1. It checks if this AWS account part of an organization with an SCP
1. If answer is No, then Go to Next Step.
1. If answer is Yes, then check if the SCP allows the action.
  1. If there is no explicit "allow", final Decision is implicit "Deny"
  1. If there is an explicit "allow", go to Next Step.

### Evaluation Logic 3: Related to Resource Policies
1. If there is no resource policy, go to Next Step.
1. If there is a resource policy, check if it allows the action.
  1. If there is an explicit "allow", final Decision is "Allow"
  1. If there's no explicit "allow", then move to Next Step.

### Evaluation Logic 4: Related to IAM Permission Boundaries
1. If there is no permission boundary for Principal identity attached, go to Next Step.
1. If there is a permission boundary attached, check if it allows the action.
  1. If there is no explicit "allow", final Decision is implicit "Deny"
  1. If there is an explicit "allow", go to Next Step.

### Evaluation Logic 5: Related to Session Based Policy
1. If user is not using Session-based policy, go to Next Step.
1. If user is using Session-based policy, check if it allows the action.
  1. If there is no explicit "allow", final Decision is implicit "Deny".
  1. If there is an explicit "allow", final decision is "Allow"

### Evaluation Logic 6: Related to Identity Based Policies
1. If there are no Identity Based Policies attached to the principal identity, final Decision is implicit "Deny"
1.If there are Identity Based Policies, check if any Identity Based Policy allows the action.
  1. If there is an explicit "allow", final Decision is "Allow"
  1. If there is no explicit "allow", final Decision is implicit "Deny"
