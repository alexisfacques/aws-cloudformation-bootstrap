# bootstrap

This AWS CloudFormation application configures resources often shared by many other services on AWS. It exports their respective Amazon Resource Names (ARNs) or logical identifiers (IDs) to help define application lineage.

It should be deployed before deploying any further AWS applications.

It includes the following resources:

- The [`lambda-testevent-schemas`](https://docs.aws.amazon.com/lambda/latest/dg/testing-functions.html) Eventbridge [schemas registry](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-eventschemas-registry.html), used to share AWS Lambda test events with other users in the same AWS account;
- IAM roles required by [CloudFormation to deploy StackSets](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/stacksets-prereqs-self-managed.html) to this account, across multiple regions.

## Installation

### Software prerequisites

- [**AWS CLI**](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-started.html);
- [**AWS SAM CLI**](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-getting-started.html).

### CloudFormation / SAM configuration

#### Template parameters

This CloudFormation template requires the following parameters to be overwritten:

Parameter name                 | Required |             Value(s)             |                                                                                                                           Description
:----------------------------- | :------: | :------------------------------: | ------------------------------------------------------------------------------------------------------------------------------------:
`TagApplication`               |    No    |      **Default:** bootstrap      |                                                            A unique, friendly name used to identify resources deployed by this stack.
`TagEnvironment`               |   Yes    |  **Allowed values:** dev / prod  | The target environment name will be tagged to all deployed resources and used to determine environment-specific configurations.

### Deploying the application

- Build and deploy the stack with AWS SAM CLI:
  ```sh
  sam build
  sam deploy --guided
  ```
