# Lab 03: Deploying to Lambda and API Gateway (Serverless)

## Goal

Add another step to your pipeline: deploy the sample application to AWS Lambda and API Gateway, aka. Serverless.

## Instructions

Make sure you are starting from the starting point for Lab 03.

```
cp lab03-serverless/starting-point/pipeline.yml deploy/pipeline.yml
cp lab03-serverless/starting-point/serverless.json infrastructure/serverless.json
```

The template `infrastructure/serverless.yml` contains the following resources and utilizes the [AWS Serverless Application Model (SAM)](https://github.com/awslabs/serverless-application-model/blob/master/versions/2016-10-31.md):

* AWS Lambda
* API Gateway
* CloudWatch alarms
* SNS topic

You need to extend the `pipeline.yml` template which already contains:

1. The sample solution from Lab 02.
1. A `Production` stage with two empty actions `CreateChangeSet` and `ApplyChangeSet`.

For the first time you need to hand over results between different stages and actions of your pipeline. Doing so is possible with a `TemplateConfiguration`. You need to complete the file `infrastructure/serverless.json`.


Commit and push your changes and watch your pipeline to build and test the application.

```
git add deploy/pipeline.yml
git add infrastructure/serverless.json
git commit -m "lab 03"
git push deploy master
```

## Help

* CloudFormation [AWS::CodePipeline::Pipeline](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-codepipeline-pipeline.html)
* CodePipeline [Pipeline Structure Reference](https://docs.aws.amazon.com/codepipeline/latest/userguide/reference-pipeline-structure.html)
* [AWS CloudFormation Configuration Properties Reference](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/continuous-delivery-codepipeline-action-reference.html)
* [AWS CloudFormation Artifacts](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/continuous-delivery-codepipeline-cfn-artifacts.html)
