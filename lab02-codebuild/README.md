# Lab 02: Building with CodeBuild

## Goal

Add a build step to your pipeline. The sample application is written in Node.js. All you need to build and test the application is [npm - the package manager for JavaScript](https://www.npmjs.com/).

## Instructions

Make sure you are starting from the starting point for Lab 02.

```
cp lab02-codebuild/starting-point/pipeline.yml deploy/pipeline.yml
```

You need to extend the `pipeline.yml` template which already contains:

1. The sample solution from Lab 01.
1. An IAM role used by CodeBuild.
1. A partial CodeBuild project resource (search for `TODO`).
1. An incomplete `Build` stage (search for `TODO`).

The application is compatible with Node.js 6.3. To build and test the app you need to execute the following commands within the `app/` directory.

```
npm install
npm test
rm -rf app/node_modules/
rm -rf app/test/
npm install --production
```

Commit and push your changes and watch your pipeline to build and test the application.

```
git add deploy/pipeline.yml
git commit -m "lab 02"
git push deploy master
```

## Help

* CloudFormation [AWS::CodeBuild::Project](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-codebuild-project.html)
* [Build Specification Reference for AWS CodeBuild](https://docs.aws.amazon.com/codebuild/latest/userguide/build-spec-ref.html)
* CloudFormation [AWS::CodePipeline::Pipeline](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-codepipeline-pipeline.html)
* CodePipeline [Pipeline Structure Reference](https://docs.aws.amazon.com/codepipeline/latest/userguide/reference-pipeline-structure.html)

An assume role policy granting CodePipeline access to a role looks like this:

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "Service": [
          "codebuild.amazonaws.com"
        ]
      },
      "Action": [
        "sts:AssumeRole"
      ]
    }
  ]
}
```
