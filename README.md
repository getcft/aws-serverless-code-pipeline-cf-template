# aws-serverless-code-pipeline-cfn-template

## Description:

This solution allows you to create a AWS Codepipline for deploying a serverless application with AWS CodeBuild triggered by a Github repo commit. The setup of this solution is fully automated via a CloudFormation template.

_***note AWS S3, API Gateway, Lambda, CodePipeline and CodeBuild as well as GitHub will incur costs**_

* [S3 pricing](https://aws.amazon.com/s3/pricing/)
* [API Gateway pricing](https://aws.amazon.com/api-gateway/pricing/)
* [Lambda pricing](https://aws.amazon.com/lambda/pricing/)
* [CodePipeline pricing](https://aws.amazon.com/codepipeline/pricing/)
* [CodeBuild pricing](https://aws.amazon.com/codebuild/pricing/)
* [GitHub pricing](https://github.com/pricing)

## Prerequisites:

* AWS account and environment configured with AWS Credentials
* Serverless Framework installed for your project (see serverless.com)
* Github account
* Github OAuth token for access to be used by AWS Codepipeline (https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/)

## See how it works:

### Step 1:
Clone this repo to your local machine or just grab the aws-serverless-code-pipeline-cfn-template.yml file.

```bash
git clone git@github.com:getcft/aws-serverless-code-pipeline-cfn-template.git
```

### Step 2:
AWS Management Console

* Login to AWS Management Console
* This example is in us-west-1 (N. California) so choose that region (note the serverless.yml file is set for us-west-1)
* Launch in CloudFormation aws-serverless-code-pipeline-cfn-template.yml (from the repo you cloned)

CloudFormation Fields

* Stack name (Enter a name to associate to your AWS CodePipline)
* CodePipelineBucketPrefix (Enter a name for the utility S3 bucket CodePipline will use)
* Environment (Choose dev stage or prod, this is an identifier)
* GitHubOAuthToken (In Github generate a OAuth token and use that here)
* GitHubRepository (The source repo for the pipeline, you can use getcft/aws-serverless-code-pipeline-cfn-template/master to test)
* Don't forget to check the box "I acknowledge that AWS CloudFormation might create IAM resources with custom names."

### Result:

The result of the CloudFormation template is that you will have built a AWS CloudPipeline along with two AWS CloudBuild projects to deploy a Hello World Serverless Express Node App (API Gateway and Lambda).

The workflow is as follows, the Github repo/branch you designated with your Serverless code will be sourced initially and upon commits, which then will trigger a AWS CloudBuild project that will package the code (you can add linting here), and send the result to another AWS CloudBuild project that will deploy the code using a deploy script.

If you used this repo as a test you can go to CloudFormation and see two templates one has "aws-serverless-express-application" in the name if you select it and look at the "Outputs" tab you will see "ServiceEndpoint" with a URL click on it and you will get a "Hello World!" message.

Anytime you commit code to the repo/branch you specified it will trigger a new build and deploy it. This will be more relevant when you use it for your own repo/branch and not the test one since you don't have access to commit to this repo.

## What key things for your personal AWS CodePipeline and Serverless project:

* buildspec-dev.yml (Instructions for AWS CodePipeline/CodeBuild to build the dev environment if that is chosen in the CloudFormation template)
* buildspec-stg.yml (Instructions for AWS CodePipeline/CodeBuild to build the stage environment if that is chosen in the CloudFormation template)
* buildspec-prod.yml (Instructions for AWS CodePipeline/CodeBuild to build the prod environment if that is chosen in the CloudFormation template)
* deploy.sh (Instructions for AWS CodePipeline to deploy the chosen environment)
* Your Serverless framework project (See serverless.com) this repo shows you the basic structure.
