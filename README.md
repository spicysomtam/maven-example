# Introduction

Maven Java build example for AWS ci/cd testing using AWS Code* services.

This example uses the following:
* CodeCommit git repo (hosting this code).
* CodePipeline that:
  * checks out this repo.
  * builds the app via CodeBuild.
  * stores the jar artifact in an S3 bucket (could use CodeArtifact).

It demonstrates a common pattern of checkout code, build it, store the artifact somewhere. 

You could add a step to the end of the pipeline to deploy it somewhere; ideally a dev environment since you should not be deploying automatically into a production environment.

# Implemenation notes

For the CodeBuild piece I used a Ubuntu docker image, which has Java 11 available.

You probably want to log the build somewhere. use CloudWatch logs, which has the benefit of showing the logging in the AWS CodeBuild Console.

I called all the various resources `maven-example`.

# Automated build of resources

Ideally you would create a terraform or cloudformation deploy to create all resources; however this takes time, effort and testing, and its much quicker to just use the AWS Console to this (with the added benefit it will setup roles and policies with the correct permissions). Time is money, etc.

I would use terraform and you would need to define the following resources:
* CodeCommit git repo.
* CodePipeline.
* CodeDeploy.
* Assortment of roles, policies and maybe some security groups to allow the various resources to talk to each other. 

If you decide to develop these raise a PR and I will add your code.

# Documentation and resources

You can follow official AWS docs. I found [this AWS video](https://www.youtube.com/watch?v=E6EBg46vvu0) very useful, although watched it after developing this (best way to learn is by doing and suppliment it with guides and videos?).