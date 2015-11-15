Tweet Searcher
========

A simple AWS Lambda function written in Java which reads data (tweets) stored in S3 and indexes it into an ElasticSearch cluster.
Used as a demo for my [Socal CodeCamp 2015](http://socalcodecamp.net/) talk

## How to use this?

### Satisfy Dependencies

Following are essential:

* [Git](http://git-scm.com/downloads)
* [Gradle](https://gradle.org/)
* [JDK 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [AWS Account](http://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-set-up.html#cli-signup)

It is recommended to also use the following for experimenting with the source code:

* [IntelliJ](https://www.jetbrains.com/idea/)
* [AWS CLI](http://docs.aws.amazon.com/cli/latest/userguide/installing.html)

### Get the source and artifacts from Github

1. `git clone https://github.com/cganoo/codecamptweetsearcher.git`
2. `cd codecamptweetsearcher/`
3. Ensure that gradle correctly fetches dependencies in the project

### Creating a JAR (suited for AWS Lambda Deployment)
1. `gradle build`
2. <b>codecamptweetsearcher-1.0-SNAPSHOT.zip</b> should now be created in <b>./build/distributions</b>

### Prerequisite AWS Resources
1. An [AWS Lambda](http://docs.aws.amazon.com/lambda/latest/dg/java-gs.html) function for reference
) which upon invocation will run your jar
2. A S3 bucket to act as the source fo events for your Lambda function
3. An ElasticSearch cluster for your Lambda function to index the received S3 events

### Updating AWS Lambda function with your jar

#### Manual Deployments:
1. When you want to push a code change rebuild your local jar.
2. Upload your local jar either directly to your Lambda function or to another S3 bucket and link it in the AWS Lambda console

<b>OR</b>
#### Auto Deployments:
1. The easiest way to update a Lambda function is to use another <i>deployer</i> Lambda Function which watches for new jars in an S3 bucket
2. This method is described in this [AWS blog](https://aws.amazon.com/blogs/compute/new-deployment-options-for-aws-lambda/)
3. Once you have set that up, all you need to do is to configure your gradle plugin to upload your jar to the S3 bucket being watched by the <i>deployer<i> Lambda function
4. Some popular ways of doing that seem to be [this](https://github.com/literalice/gradle-aws-s3-sync) and [this](https://github.com/classmethod-aws/gradle-aws-plugin)

### Highlights

* The Application class implements the predefined [RequestHandler](http://docs.aws.amazon.com/lambda/latest/dg/java-handler-using-predefined-interfaces.html) interface from AWS Lambda
* [Jest](https://github.com/searchbox-io/Jest) is used to index retrieved data into ElasticSearch cluster

### License

codecamptweetsearcher is licensed under the MIT license. It is primarily intended for fun and instructive purposes.
Use this at your own risk.

## Author

Chaitanya Ganoo
www.linkedin.com/in/cganoo
