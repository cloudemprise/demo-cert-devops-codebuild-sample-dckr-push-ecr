# demo-cert-devops-codebuild-sample-dckr-push-ecr

> AWS CodeCommit / GitHub Repository used for the Hands-On Demonstrations in connection with the AWS Certified DevOps Engineer Professional Exam Study course.

![](https://codebuild.eu-central-1.amazonaws.com/badges?uuid=eyJlbmNyeXB0ZWREYXRhIjoiazhSSEZCeE1RSUowM3lUVTUyd0lZMDFGYlMzaEl1c1QycGpRRFVSNll3bkVtUTdoQWN6Y2RKc1ZaMjN4RlE2MjVDeUZUNzJwamdDTm5uVVlRbCsxT1lJPSIsIml2UGFyYW1ldGVyU3BlYyI6IjVKalRJc1RpVGlrZXZlbzEiLCJtYXRlcmlhbFNldFNlcmlhbCI6MX0%3D&branch=main)

---

The repository contains artifacts and reference material related to an AWS CodeBuild build project and its auxillary components. These components build a Docker image that is then pushed to an Amazon Elastic Container Registry (Amazon ECR) image repository.

Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse
cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.

### Note: 

- Point 1
- Point 2

**Reference:**

- AWS CodeBuild - [Docker sample for CodeBuild](https://docs.aws.amazon.com/codebuild/latest/userguide/sample-docker.html)

- DockerHub - [Use multi-stage builds](https://docs.docker.com/develop/develop-images/multistage-build/)

- AWS ECR - [Creating a private repository](https://docs.aws.amazon.com/AmazonECR/latest/userguide/repository-create.html)

- AWS ECR - [Image scanning](https://docs.aws.amazon.com/AmazonECR/latest/userguide/image-scanning.html)

- Clair - [Open Source Application Container Vulnerabilities Scanner](https://github.com/quay/clair)

---

### Amazon ECR Private Repository
> #### demo-cert-devops/codebuild-sample/dckr-push-ecr

##### Push commands:

Use the following steps to authenticate and push an image to your repository. For additional registry authentication methods, including the Amazon ECR credential helper, see [Registry Authentication](https://docs.aws.amazon.com/AmazonECR/latest/userguide/Registries.html#registry_auth) .

1. Retrieve an authentication token and authenticate your Docker client to your registry.
Use the AWS CLI:

`aws ecr get-login-password --region eu-central-1 | docker login --username AWS --password-stdin 311674589786.dkr.ecr.eu-central-1.amazonaws.com`

2. Build your Docker image using the following command. For information on building a Docker file from scratch see the instructions [here](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/docker-basics.html) 
. You can skip this step if your image is already built:

`docker build -t demo-cert-devops/codebuild-sample/dckr-push-ecr .`

3. After the build completes, tag your image so you can push the image to this repository:

`docker tag demo-cert-devops/codebuild-sample/dckr-push-ecr:latest 311674589786.dkr.ecr.eu-central-1.amazonaws.com/demo-cert-devops/codebuild-sample/dckr-push-ecr:latest`

---

> ### Relavent APIs:

> #### _AWS CodeBuild_

> [create-project](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/codebuild/create-project.html)

> [list-projects](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/codebuild/list-projects.html)

> [batch-get-projects](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/codebuild/batch-get-projects.html)


> #### _Amazon ECR_

> [create-repository](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/ecr/create-repository.html)

> [get-login-password](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/ecr/get-login-password.html)
