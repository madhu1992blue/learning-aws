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
