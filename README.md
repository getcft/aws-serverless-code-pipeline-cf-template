# aws-serverless-code-pipeline-cfn-template

## Description

This solution allows you to create a AWS Codepipline for deploying a serverless application with AWS CodeBuild triggered by a Github repo commit. The setup of this solution is fully automated via a CloudFormation template.

## Prerequisites:

* AWS account and environment configured with AWS Credentials
* Serverless Framework installed
* Github account
* Github OAuth token for access via AWS Codepipeline


## Step 1 Clone this repo to your local machine

```bash
git clone git@github.com:[your-github-user]/aws-serverless-code-pipeline-cfn-template.git
```

## Step 3 AWS Management Console

* Login to AWS Management Console
* Launch in CloudFormation aws-serverless-code-pipeline-cfn-template.yaml (from the repo you cloned)

### CloudFormation Fields:

* Stack name (enter a name to associate to your AWS CodePipline)
* CodePipelineBucketPrefix (enter a name for the utility S3 bucket codepipline will use)
* Environment (choose dev stage or prod)
* GitHubOAuthToken (in Github generate a OAuth token and use that here)
* GitHubRepository (the source repo for the pipeline, you can use getcft/aws-serverless-code-pipeline-cfn-template/master to test)
* Don't forget to check the box "I acknowledge that AWS CloudFormation might create IAM resources with custom names."
