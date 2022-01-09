## demo-cert-devops-codebuild-sample-dckr-push-ecr

> AWS CodeCommit / GitHub Repository used for the Hands-On Demonstrations in connection with the AWS Certified DevOps Engineer Professional Exam Study course.

![](https://codebuild.eu-central-1.amazonaws.com/badges?uuid=eyJlbmNyeXB0ZWREYXRhIjoidnJHL1VaWmxQZmZDZWx6NGtZWFBqTlhIZnlHOHJjUCtkOWRtOFU5b29ORUpmSStRWFNxMWdrZnY3L2NTb3VDelNXbUR2MHFVaTQzeHBVczE5VFdSUmEwPSIsIml2UGFyYW1ldGVyU3BlYyI6IkZodDF2Vks0alJjVlR3ZFUiLCJtYXRlcmlhbFNldFNlcmlhbCI6MX0%3D&branch=main)

---

#### Overview

&nbsp;

The repository contains artifacts and reference material related to an AWS CodeBuild build project and its auxiliary components. These components build and track a Docker image that is then pushed to an Amazon Elastic Container Registry (Amazon ECR) image repository.

&nbsp;

#### Multi-Stage Docker Build Feature

This build architecture makes use of the Multi-Stage Docker Build Feature, which produces an optimized Docker Image, efficiently building small images which improves the developer experience tremendously.

&nbsp;

#### AWS CodeBuild service role

For a particular build project, it is convenient to automatically create an AWS CodeBuild Project service role by enabling the following from the AWS Console during project creation:

`Allow AWS CodeBuild to modify this service role so it can be used with this build project` 

This produces a policy of least-privilege but in this particular case, in order to push an image to an Amazon ECR repository the AWS CodeBuild service role will need extra authorizations to do so. This is simply achieved by way of an inline policy statement manually attached to the automatically created policy, giving the AWS CodeBuild service the necessary permissions to do so. An example of this inline policy is included here for reference.

&nbsp;

#### AWS CodeBuild Environment Variables

Pushing a Docker image to an Amazon ECR repository from AWS CodeBuild also requires the following AWS CodeBuild build environment variables: 

`AWS_DEFAULT_REGION = region-ID`

`AWS_ACCOUNT_ID = account-ID`

`IMAGE_TAG = latest`

`IMAGE_REPO_NAME = Amazon-ECR-repo-name`

&nbsp;

#### Amazon ECR Private Repository
##### demo-cert-devops/codebuild-sample/dckr-push-ecr

###### Push commands:

Use the following steps to authenticate and push an image to your repository. For additional registry authentication methods, including the Amazon ECR credential helper, see [Registry Authentication](https://docs.aws.amazon.com/AmazonECR/latest/userguide/Registries.html#registry_auth) .

1. Retrieve an authentication token and authenticate your Docker client to your registry.
Use the AWS CLI:

`aws ecr get-login-password --region eu-central-1 | docker login --username AWS --password-stdin 311674589786.dkr.ecr.eu-central-1.amazonaws.com`

2. Build your Docker image using the following command. For information on building a Docker file from scratch see the instructions [here](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/docker-basics.html) 
. You can skip this step if your image is already built:

`docker build -t demo-cert-devops/codebuild-sample/dckr-push-ecr .`

3. After the build completes, tag your image so you can push the image to this repository:

`docker tag demo-cert-devops/codebuild-sample/dckr-push-ecr:latest 311674589786.dkr.ecr.eu-central-1.amazonaws.com/demo-cert-devops/codebuild-sample/dckr-push-ecr:latest`

&nbsp;

#### Note: 

- This sample was tested referencing golang:1.12.
- The CodeBuild project environment must be configured in Privileged Mode.
- A bash script has been included to reconfigure the git remotes to push to multiple git repositories, i.e. to GitHub and AWS CodeCommit.

---

#### Reference:

- AWS CodeBuild - [Docker sample for CodeBuild](https://docs.aws.amazon.com/codebuild/latest/userguide/sample-docker.html)

- AWS CodeBuild - [Environment variables in build environments ](https://docs.aws.amazon.com/codebuild/latest/userguide/build-env-ref-env-vars.html)

- AWS ECR - [Creating a private repository](https://docs.aws.amazon.com/AmazonECR/latest/userguide/repository-create.html)

- Docker CLI - [Runtime privilege and Linux capabilities](https://docs.docker.com/engine/reference/run/#runtime-privilege-and-linux-capabilities)

- DockerHub - [Use multi-stage builds](https://docs.docker.com/develop/develop-images/multistage-build/)

- AWS ECR - [Image scanning](https://docs.aws.amazon.com/AmazonECR/latest/userguide/image-scanning.html)

- Clair - [Open Source Application Container Vulnerabilities Scanner](https://github.com/quay/clair)

- Blog Post - [Builder pattern vs. Multi-stage builds in Docker](https://blog.alexellis.io/mutli-stage-docker-builds/)

&nbsp;

#### Relevant APIs:

> ##### _AWS CodeBuild_

> [create-project](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/codebuild/create-project.html)

> [list-projects](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/codebuild/list-projects.html)

> [batch-get-projects](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/codebuild/batch-get-projects.html)


> ##### _Amazon ECR_

> [create-repository](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/ecr/create-repository.html)

> [get-login-password](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/ecr/get-login-password.html)
