## AWS
## Intro
- Batasan : tidak membahas EC2/ECS
- mambangun serverless backend cloud-native tools/services, API driven development process
- Amazon API gateway --> serverless API Hosting
- Amazon Lambda --> serverless compute
- Amazon Cogneto --> serverless auth
## Overview
- AWS services used: Amazon S3, Amazon API Gateway, Amazon Cognito, AWS Lambda, AWS Step Functions, AWS X-Ray, and Amazon Comprehend.
  - Lab 1:
    - Create a static  **Amazon S3** website with a bucket policy that restricts access to the website via IP Address.
    - The website will be created using the **AWS SDK** and **AWS CLI**.
  - Lab 2:
    - Setup mock backend API using **Amazon API Gateway** REST APIs.
    - You will setup 3 API endpoints using the AWS SDK and AWS CLI, these endpoints will respond to requests with mocked data.
    - You will test this mock API using the website setup in Lab 1 make AJAX calls to the mock API.
  - Lab 3:
    - Secure the API that was built in Lab 2 by adding authentication via **Amazon Cognito** User Pools.
  - Lab 4:
    - Create **AWS Lambda** functions to host the backend for your API.
    - You will then configure the secured API built in Lab 3 to trigger to the lambda functions, instead of using mock integrations.
  - Lab 5:
    - Create an asynchronous state machine using **AWS Step Functions** for a reporting feature of the API.
    - You will then configure the API to run this state machine when a request hits an API endpoint you built in the previous labs.
  - Lab 6:
    - Use **AWS X-Ray** to trace requests through your distributed application.
    - You will also make improvements to your application using various AWS service features like Amazon API Gateway Response Caching, as well as code modifications.
    - Then you will test and view the performance improvements in the AWS X-Ray Console.

## Building Our Environment
- Architecture Cloud
- ![serverless](https://user-images.githubusercontent.com/24581953/116175264-2d024f80-a73a-11eb-9a4a-4c17709ecb02.jpg)
- AWS Cloud9

## AWS CLIs and APIs
- ![aws-cli](https://user-images.githubusercontent.com/24581953/116177179-8ddf5700-a73d-11eb-9292-009cc66631f9.jpg)
- Docs: Cloud9, AWS APIs, AWS CLI
  - AWS CLI
    - [AWS CLI info](https://aws.amazon.com/cli/)
    - [AWS CLI install](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-install.html)
    - [AWS CLI config](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-configure.html)
  - AWS Cloud9
    - [Cloud9 User guide](https://docs.aws.amazon.com/cloud9/latest/user-guide/welcome.html)
    - [Temporary Credentials](https://docs.aws.amazon.com/cloud9/latest/user-guide/how-cloud9-with-iam.html#sec-auth-and-access-control-temporary-managed-credentials)
    - [Cloud9 access key](https://docs.aws.amazon.com/general/latest/gr/aws-access-keys-best-practices.html)
  - IAM
    - https://docs.aws.amazon.com/cli/latest/reference/iam/
- AWS SDK Exploration (Python)
