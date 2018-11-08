# Lab 04: Deploying to ECS

## Goal

Add another step to your pipeline: deploy the sample application to Elastic Container Service (ECS).

## Instructions

Make sure you are starting from the starting point for Lab 04.

```
cp lab04-ecs/starting-point/pipeline.yml deploy/pipeline.yml
cp lab04-ecs/starting-point/ecs.json infrastructure/ecs.json
```

The template `infrastructure/ecs.yml` contains the following resources:

* ECS Service
* ECS Task Definition
* Application Load Balancer
* Auto Scaling of the ECS Service
* CloudWatch alarms + SNS topic
* IAM roles and security groups

You need to extend the `pipeline.yml` template which already contains:

1. The sample solution from Lab 02.
1. The IAM role `ImageCodeBuildRole` which is needed for CodeBuild when building and publishing a Docker image.
1. A `Production` stage with an empty action `Deploy` (search for `TODO`).

To be able to deploy to ECS, you need to add the following parts to your deployment:

1. An Elastic Container Registry (ECR) for the Docker images.
1. A CodeBuild project to build and publish the Docker image.
1. An additional action for your CodePipeline to trigger the CodeBuild project building the Docker image.
1. An additional action for your CodePipeline to deploy your ECS service via CloudFormation.

Commit and push your changes and watch your pipeline to build and test the application.

```
git add deploy/pipeline.yml
git add infrastructure/ecs.json
git commit -m "lab 04"
git push deploy master
```

## Help

* CloudFormation [AWS::ECR::Repository](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-ecr-repository.html)
* CloudFormation [AWS::CodeBuild::Project](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-codebuild-project.html)
* [Build Specification Reference for AWS CodeBuild](https://docs.aws.amazon.com/codebuild/latest/userguide/build-spec-ref.html)
* CloudFormation [AWS::CodePipeline::Pipeline](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-codepipeline-pipeline.html)
* CodePipeline [Pipeline Structure Reference](https://docs.aws.amazon.com/codepipeline/latest/userguide/reference-pipeline-structure.html)
* [AWS CloudFormation Configuration Properties Reference](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/continuous-delivery-codepipeline-action-reference.html)
* [AWS CloudFormation Artifacts](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/continuous-delivery-codepipeline-cfn-artifacts.html)
* CodeBuild [Multiple Input Sources and Output Artifacts Sample](https://docs.aws.amazon.com/codebuild/latest/userguide/sample-multi-in-out.html)
