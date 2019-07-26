# learn-codepipeline

Labs helping you to learn AWS CodePipeline within a day. Labs are based on the [AWS Velocity Series](https://cloudonaut.io/aws-velocity-series/).

Are you looking for an instructor-led workshop based on these labs? Say [hello@widdix.net](mailto:hello@widdix.net).

> Raise the VPCs per region limit if you run this lab with a larger group of people!

## Labs

* [Lab 01: Deploying a CloudFormation template](lab01-cloudformation/)
* [Lab 02: Building with CodeBuild](lab02-codebuild/)
* [Lab 03: Deploying to Lambda and API Gateway (Serverless)](lab03-serverless/)
* [Lab 04: Deploying to ECS](lab04-ecs/)

## Setup your personal lab environment

Clone this repository on your local machine.

```
git clone https://github.com/widdix/learn-codepipeline.git
```

Create a CodeCommit repository. Replace `$user` with your name (e.g. `andreas`).

```
aws codecommit create-repository --repository-name learn-codepipeline-$user
```

The command will return some information about your repository.
```
{
    "repositoryMetadata": {
        "accountId": "111111111111",
        "repositoryId": "c1998fd8-2c78-4a73-984c-53d588a6b237",
        "repositoryName": "learn-codepipeline-andreas",
        "lastModifiedDate": 1541665280.947,
        "creationDate": 1541665280.947,
        "cloneUrlHttp": "https://git-codecommit.eu-west-1.amazonaws.com/v1/repos/learn-codepipeline-andreas",
        "cloneUrlSsh": "ssh://git-codecommit.eu-west-1.amazonaws.com/v1/repos/learn-codepipeline-andreas",
        "Arn": "arn:aws:codecommit:eu-west-1:111111111111:learn-codepipeline-andreas"
    }
}
```

```
git remote add deploy https://git-codecommit.eu-west-1.amazonaws.com/v1/repos/learn-codepipeline-andreas
```

Edit `.git/config` and add.

```
[credential]
    helper =
    helper = !aws codecommit credential-helper $@
    UseHttpPath = true
```

```
git push deploy master
```

## Setup the global infrastructure for all labs

**Typically the following steps are taken care of by the workshop instructor only.**

Adjust cluster size according to number of workshop participants.

```
aws cloudformation create-stack --stack-name vpc-2azs --template-url https://s3-eu-west-1.amazonaws.com/widdix-aws-cf-templates-releases-eu-west-1/stable/vpc/vpc-2azs.yaml

aws cloudformation create-stack --stack-name ecs-cluster --template-url https://s3-eu-west-1.amazonaws.com/widdix-aws-cf-templates-releases-eu-west-1/stable/ecs/cluster.yaml --parameters ParameterKey=ParentVPCStack,ParameterValue=vpc-2azs ParameterKey=InstanceType,ParameterValue=m5.large ParameterKey=MaxSize,ParameterValue=2 ParameterKey=MinSize,ParameterValue=2, ParameterKey=DesiredCapacity,ParameterValue=2 --capabilities CAPABILITY_IAM
```

## More Labs

We offer AWS workshops tailored to your needs. See [widdix/learn-*](https://github.com/widdix?q=learn-) for more labs.
