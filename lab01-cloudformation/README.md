# Lab 01: Deploying a CloudFormation template

## Goal

Create a CodePipeline that fetches your source code from CodeCommit and updates itself based on a CloudFormation template `deploy/pipeline.yml`.

## Instructions

Make sure you are starting from the starting point for Lab 01.

```
cp lab01-cloudformation/starting-point/pipeline.yml deploy/pipeline.yml
```

Extend the CloudFormation template at `deploy/pipeline.yml` with the following resources.

1. A S3 bucket to store pipeline artifacts.
1. An IAM role for CodePipeline with managed policy `AdministratorAccess`.
1. An IAM role for CloudFormation with managed policy `AdministratorAccess`.
1. A CodePipeline with the following stages
    1. Source: Fetch source code from CodeCommit
    1. Pipeline: Deploy the CloudFormation template `deploy/pipeline.yml`.

Create a CloudFormation stack based on your template. Replace `$user` with your name (e.g. `andreas`).

```
aws cloudformation create-stack --stack-name learn-codepipeline-$user --template-body file://deploy/pipeline.yml --parameters ParameterKey=RepositoryName,ParameterValue=learn-codepipeline-$user --capabilities CAPABILITY_IAM
```

The pipeline should fail, as you haven't pushed your changes yet.

```
git add deploy/pipeline.yml
git commit -m "lab 01"
git push deploy master
```

This time your pipeline should succeed!

## Help

* CloudFormation [AWS::S3::Bucket](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-s3-bucket.html)
* CloudFormation [AWS::IAM::Role](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-iam-role.html)
* CloudFormation [AWS::CodePipeline::Pipeline](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-codepipeline-pipeline.html)
* CodePipeline [Pipeline Structure Reference](https://docs.aws.amazon.com/codepipeline/latest/userguide/reference-pipeline-structure.html)
