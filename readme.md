# Demos for "Level Up Your Web Apps With Amazon Web Services"

There are four requirements for getting these demos working. I know that sounds like a lot, but we're dealing with a series of external services in multiple lanaguages in these demos, and each must be set up correctly.

1. Add the AWS SDK .jar and related files to your CF install.
2. Install boto and make the Python demo files executable.
3. Set up your own AWS credentials and add them to awsCredentials.cfc.
4. Set up your own copies of the required resources in SNS, Lambda, and DynamoDB.

### Requirement One: The AWS SDK .jar and Related Files

The demos in this repo require that you have the following .jar files in your /coldfusion/lib/ directory:

- aws-java-sdk-1.10.30 or later
- jackson-annotations
- jackson-core
- jackson-databind
- joda-time

All of these files can be downloaded from [https://aws.amazon.com/sdk-for-java/](https://aws.amazon.com/sdk-for-java/) Files other than the actual SDK .jar itself can be found in the /third-party directory within the SDK download.

### Requirement Two: boto (if you want to run any Python demos)

In order to run the Python SNS demos from this application, you will need to:

1. [Install boto](http://boto.cloudhackers.com/en/latest/getting_started.html)
2. Run chmod a+x on python/sns/pythonInvoke.sh, subscribeViaEmail.py, and publishToSNS.py 

The application will run fine without doing any of this. The Python demos just won't run.

If you're not running a CFML engine, you can run the Python demos from the command line if you have boto installed and have configured your AWS credentials.

### Requirement Three: Your Own AWS Credentials

You have to create your own AWS account and provide both the AccessKey and SecretKey in model/awsCredentials.cfc.

If you want to run the Python demos, you need to [configure boto with your AWS credentials](http://boto.cloudhackers.com/en/latest/boto_config_tut.html). If you're on the Mac, it's easiest to use /etc/boto.cfg. 

The account for which you are providing credentials must also have permissions for the following services:

- SNS
- Lambda
- CloudWatch (for Lambda logging)
- DynamoDB

For more infomration about IAM accounts, roles, and permissions, please review the [IAM guide](http://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html).

### Requirement Four: Your Own AWS Resources

You need to set up the following resources within AWS for these demos to work:

1. SNS - create a topic to which messsages can be sent. The ARN of this topic must be added to the top of sns.cfm, python/sns/subscribeViaEmail.py, and python/sns/publishToSNS.py.
2. Lambda - create a Lambda function using the code in lambdaJSFunctions/lambda-returnDataToCaller.js. The name of the function must be added to the top of lambda.cfm. Other Lambda functions from the presentation are not called from this application. You can, however, add them to Lambda using the source code in this repo.
3. DynamoDB - create a DynamoDB table with a primary key (hash key) of "userID" (String) and a sort key (range key) of "epochTime" (Number). The table name must be added to the top of dynamodb.cfm.

Remember, the AWS docs are pretty great. Use the [Java API Reference](http://docs.aws.amazon.com/AWSJavaSDK/latest/javadoc/index.html) often, as it'll tell you almost everything you need to know for working with a particular AWS service.

Enjoy!