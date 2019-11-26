DotnetLambda API
==================================================

DotnetLambda.Api is an ASP.NET core web API that runs serverless on AWS API Gateway and Lambda
It utilizes the AWS Sam framework for building and deploying serverless applications. The SAM
template (template.yml) compliles to CloudFormation and all the AWS resources are managed in
this project as IaaC.

What's Here
-----------

This sample includes:

* DotnetLambda.Api - The main ASP.NET Web API project with Lambda entry point
* DotnetLambda.Api.Tests - The test project for endpoints in the DotnetLambda.Api. These are automatically run
	in CodePipeline.
* README.md - this file
* appspec.yml - this file is used by AWS CodeDeploy when deploying the web service to EC2
* buildspec.yml - this file is used by AWS CodeBuild to build the web service
* template.yml - this file contains the description of AWS resources used by AWS SAM and
	CloudFormation to deploy your infrastructure
* template-configuration.json - this file contains the project ARN with placeholders used for tagging resources with the project ID
* codepipeline-template.yml - the cloudformation template for this solutions CI/CD pipeline
* scripts/ - this directory contains scripts used by AWS CodeDeploy when
  installing and deploying your service on the Amazon EC2 instance (not used for Lambda deployments)


Getting Started
---------------

# View the CodeStar dashboard
https://console.aws.amazon.com/codestar/home?region=us-east-1#/projects/DotnetLambda-api/dashboard

# Adding new developers to the project
https://console.aws.amazon.com/codestar/home?region=us-east-1#/projects/DotnetLambda-api/team

# Code repo
https://console.aws.amazon.com/codesuite/codecommit/repositories/DotnetLambda-Api/browse?region=us-east-1

# CI/CD pipeline
https://console.aws.amazon.com/codesuite/codepipeline/pipelines/DotnetLambda-api-Pipeline/view?region=us-east-1

# API Gateway
https://console.aws.amazon.com/apigateway/home?region=us-east-1#/apis/d4dg0zzeg3/resources/ro0puhba7k

# Debugging Locally via Kestrel

These directions assume you want to develop on your local computer, and not
from the Amazon EC2 instance itself. If you're on the Amazon EC2 instance, the
virtual environment is already set up for you, and you can start working on the
code.

To work on the sample code, you'll need to clone your project's repository to your
local computer. If you haven't, do that first. You can find instructions in the
AWS CodeStar user guide.

1. Install dotnet.  See https://www.microsoft.com/net/core

2. Build the service.

        $ dotnet restore
        $ dotnet build

3. Run Kestrel server.

        $ dotnet run

4. Open http://localhost:5000/ in a web browser to view your service.


# Debugging Locally via SAM and local API Gateway

		$ sam local start-api

Adding new API Endpoints
------------------

1. Create a controller method in the .NET Web API just like normal. Open an existing controller in
DotnetLambda.Api/Controllers/ or create a new controller for a collection of new endpoints.

2. Define the API endpoint in the template.yml using SAM or native CloudFormation.
	see: AWS::Serverless::Function
	https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-sam-template.html

What Do I Do Next?
------------------

Once you have a virtual environment running, you can start making changes to
the sample ASP.NET Core web service. We suggest making a small change to
/DotnetLambda.Api/Controllers/ValuesController.cs first, so you can see how
changes pushed to your project's repository are automatically picked up by your
project pipeline and deployed to the Amazon EC2 instance. (You can watch the
pipeline progress on your project dashboard.) Once you've seen how that works,
start developing your own code, and have fun!

To run your tests locally, go to the root directory of the sample code and run the
`dotnet vstest DotnetLambda.Api.Tests/test_output/DotnetLambda.Api.Tests.dll` command,
which AWS CodeBuild also runs through your `buildspec.yml` file.

To test your new code during the release process, modify the existing tests or add tests
to the tests directory. AWS CodeBuild will run the tests during the build stage of your
project pipeline. You can find the test results in the AWS CodeBuild console.

Learn more about AWS CodeBuild and how it builds and tests your application here:
https://docs.aws.amazon.com/codebuild/latest/userguide/concepts.html

Learn more about AWS CodeStar by reading the user guide. Ask questions or make
suggestions on our forum.

User Guide: http://docs.aws.amazon.com/codestar/latest/userguide/welcome.html

Forum: https://forums.aws.amazon.com/forum.jspa?forumID=248

How Do I Add Template Resources to My Project?
------------------

To add AWS resources to your project, you'll need to edit the `template.yml`
file in your project's repository. You may also need to modify permissions for
your project's worker roles. After you push the template change, AWS CodeStar
and AWS CloudFormation provision the resources for you.

See the AWS CodeStar user guide for instructions to modify your template:
https://docs.aws.amazon.com/codestar/latest/userguide/how-to-change-project.html#customize-project-template

What Should I Do Before Running My Project in Production?
------------------

AWS recommends you review the security best practices recommended by the framework
author of your selected sample application before running it in production. You
should also regularly review and apply any available patches or associated security
advisories for dependencies used within your application.

Best Practices: https://docs.aws.amazon.com/codestar/latest/userguide/best-practices.html?icmpid=docs_acs_rm_sec
