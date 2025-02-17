# Lambda - CICD Workflow

- Created a basic Lambda function in AWS Console.
- Created a GitHub Actions Workflow to automatically deploy changes made to the Lambda function.
  - Used GitHub Secrets to store the AWS Credentials used to authenticate and access AWS.
- Changes made in the lambda directory on the main branch will trigger the workflow.
- Result is that the updated Lambda function will be deployed to AWS.

## Workflow Architecture

![Lambda - CICD Workflow Architecture](/images/github-actions-lambda-workflow.png)

[Lambda - CICD Workflow Code](.github/workflows/lambda-deploy.yaml)

[Lambda Function](/lambda/lambda_function.py)

# PR Event - CICD for CloudFormation Test Stacks

- Workflow to automatically validate and test a CloudFormation Template for an S3 Bucket creation when a Pull Request is opened or updated.
- A Push event to GitHub will trigger a pull request, this will kickoff the GitHub Actions Workflow.
- AWS credentials for authenticating and accessing AWS will be stored in GitHub Secrets.
- The Runner will do the setup with AWS CLI to configure the credentials.
- The CloudFormation template will be validated on correctness.
- Once validated, a test S3 Bucket, that is defined in the CloudFormation Stack will be deployed to AWS.
- When deployed, the GitHub Actions bot will leave a comment on the PR.
  - Will tell test results, the name of the PR, and the name of the CloudFormation Stack.
- After merging the PR to the main branch, the test CloudFormation Stack will be deleted.

## Workflow Architecture

![PR Event - CICD Workflow Architecture](/images/pr-event-cloudformation-cicd.png)

[PR Event - CICD Workflow Code](.github/workflows/cfn-validate-pr.yaml)
