# aws-serverless-code-pipeline-cfn-template

## Description

This solution allows you to create a AWS Codepipline for deploying a serverless application with AWS CodeBuild triggered by a Github repo commit. The setup of this solution is fully automated via a CloudFormation template.

## Prerequisites:

* AWS account and environment configured with AWS Credentials
* Serverless Framework installed (see serverless.com)
* Github account
* Github OAuth token for access via AWS Codepipeline

## See how it works:

### Step 1
Clone this repo to your local machine or just grab the aws-serverless-code-pipeline-cfn-template.yml file.

```bash
git clone git@github.com:getcft/aws-serverless-code-pipeline-cfn-template.git
```

### Step 2
AWS Management Console

* Login to AWS Management Console
* Launch in CloudFormation aws-serverless-code-pipeline-cfn-template.yml (from the repo you cloned)

### CloudFormation Fields:

* Stack name (Enter a name to associate to your AWS CodePipline)
* CodePipelineBucketPrefix (Enter a name for the utility S3 bucket CodePipline will use)
* Environment (Choose dev stage or prod, this is an identifier)
* GitHubOAuthToken (In Github generate a OAuth token and use that here)
* GitHubRepository (The source repo for the pipeline, you can use getcft/aws-serverless-code-pipeline-cfn-template/master to test)
* Don't forget to check the box "I acknowledge that AWS CloudFormation might create IAM resources with custom names."

### Result:

The result of the steps above is that you will have built a AWS CloudPipeline along with two AWS CloudBuild projects to deploy a Hello World Serverless Express Node App (API Gateway and Lambda). The workflow is the Github repo/branch you designated with your Serverless code will be sourced initially and upon commits, which then will trigger a AWS CloudBuild project that will package the code (you can add linting during this step too) and send the result to another AWS CloudBuild project that will deploy the code using a deploy script.

## What key things you need for your personal Serverless project and AWS CodePipeline:

* buildspec-dev.yml (Instructions for AWS CodePipeline to build the dev environment if that is chosen in the CloudFormation template)
* buildspec-stg.yml (Instructions for AWS CodePipeline to build the stage environment if that is chosen in the CloudFormation template)
* buildspec-prod.yml (Instructions for AWS CodePipeline to build the prod environment if that is chosen in the CloudFormation template)
* deploy.sh (Instructions for AWS CodePipeline to deploy the chosen environment)
* Your Serverless framework project (See serverless.com) this repo shows you the basic structure.
