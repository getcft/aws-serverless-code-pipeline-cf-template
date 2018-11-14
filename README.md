# aws-serverless-code-pipeline-cfn-template

## Description

This solution allows you to create a AWS Codepipline for deploying a serverless application with AWS CodeBuild triggered by a Github repo commit. The setup of this solution is fully automated via a CloudFormation template.

## Prerequisites:

* AWS account and environment configured with AWS Credentials
* Serverless Framework installed
* Github account
* Github OAuth token for access via AWS Codepipeline

## See how it works

## Step 1
Clone this repo to your local machine or just grab the aws-serverless-code-pipeline-cfn-template.yml file.

```bash
git clone git@github.com:getcft/aws-serverless-code-pipeline-cfn-template.git
```

## Step 2
AWS Management Console

* Login to AWS Management Console
* Launch in CloudFormation aws-serverless-code-pipeline-cfn-template.yml (from the repo you cloned)

### CloudFormation Fields:

* Stack name (Enter a name to associate to your AWS CodePipline)
* CodePipelineBucketPrefix (Enter a name for the utility S3 bucket codepipline will use)
* Environment (Choose dev stage or prod)
* GitHubOAuthToken (In Github generate a OAuth token and use that here)
* GitHubRepository (The source repo for the pipeline, you can use getcft/aws-serverless-code-pipeline-cfn-template/master to test)
* Don't forget to check the box "I acknowledge that AWS CloudFormation might create IAM resources with custom names."

## What you need for your Serverless project and AWS CodePipeline

* buildspec-dev.yml (Instructions for AWS CodePipeline to build the dev environment if that is chosen in the CloudFormation template)
* buildspec-stg.yml (Instructions for AWS CodePipeline to build the stage environment if that is chosen in the CloudFormation template)
* buildspec-prod.yml (Instructions for AWS CodePipeline to build the prod environment if that is chosen in the CloudFormation template)
* deploy.sh (Instructions for AWS CodePipeline to deploy the chosen environment)
* Your Serverless framework project (See serverless.com)
