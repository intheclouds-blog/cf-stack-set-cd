# cf-stack-set-cd
Cross-region and cross-account continuous Lambda deployment using AWS CloudFormation Stack Sets

## Setup steps

1. Use CloudFormation to provision a CodeCommmit repo, CodePipeline pipeline, and CodeBuild project for the Lambda function

    ```
    aws cloudformation deploy --template-file ./template-devtools.yml --stack-name hello-lambda-devtools --capabilities CAPABILITY_NAMED_IAM --parameter-overrides FunctionName=hello
    ```

2. Add the necessary Stack Set permissions as described here:

    https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/stacksets-prereqs.html

3. Commit and push the code for the Hello lambda function to the created CodeCommit repository. This will start a build and use the `buildspec.yml` and `template.yml` file to provision the function. 

**NOTE:** See the comments in `buildspec.yml` regarding provisioning the CloudFormation Stack Set for the Lambda function on the first run of the pipeline.


### Dev Dependencies

* .NET Core 2.1
* Amazon.Lambda.Core 1.0.0
* Amazon.Lambda.Serialization.Json 1.3.0
* Amazon.Lambda.Tools 2.2.0
* Newtonsoft.Json 11.0.2

### Test Dependencies

* xUnit.net 2.3.1
* Amazon.Lambda.TestUtilities 1.0.0
* Microsoft.NET.Test.Sdk 15.5.0
