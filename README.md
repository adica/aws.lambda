# AWS lambda functions introduction

## What is AWS lambda anyway?
In 2015 Amazon introduced us [AWS Lambda functions](http://docs.aws.amazon.com/lambda/latest/dg/welcome.html) - a serverless compute platform for stateless code execution in response to triggers.


Basically - the code is split into small stateless functions (microservices) that are executed in response to triggers. Those triggers might be:
- HTTP request to specific end-point
- File PUT event on s3 bucket
- AWS SDK event call
- New event on SQS (AWS queue system)


When using Lambda functions we significantly reduce the server maintenance complexability. There is no need to launch server instance, to configure, to handle scaling, monitoring, and security, to handle versioning etc. Instead, we only need to configure these functions with the AWS interface and deploy the code into it (by simply uploading zip file).


Then we can keep working on developing new features or improving existing ones, without worrying about all these infrastructure issues.


## How to use AWS lambda

 AWS gives us simple function signature with 3 parameters:
 
 ```javascript
 exports.handler = (event, context, callback) => {
    //event - the event that triggers this function
    //context - some data about the context this function run at
    //callback - to execute when we want to resolve it.
    
    // write your logic here
 };
 ```
All we need is to write our logic into this function. We can use any needed NPM package, and write our code like any other microservice on node environment (we note that AWS lambda supports many other [languages](http://docs.aws.amazon.com/lambda/latest/dg/current-supported-versions.html) - but this is out of the scope of this post).


## Usage example
Here is a simple example of a Lambda function that is triggered when a PDF file is uploaded on s3, and we want to create a thumb out of it:

![pdf-to-thumb lambda function](http://rawdata.adicarmel.com.s3.amazonaws.com/tmp/lambda-pdf-to-thumb.png)


This function does the following:
- read the file path and name from the event (lines 7-8)
- go to s3 bucket and retrieve this file (line 11)
- use 'gm' (a package that wraps 'image-magic' - a tool for image processing) to convert PDF to thumb PNG image (lines 15-18)
- upload the thumb PNG image back to s3 bucket (line 22)
- use 'context.done' to resolve the function with or without an error

And that's it! 

This code will be highly available and secured on the AWS server without the need to set up and maintain server.

## Lambda pros

- Our Code will be highly secured on AWS servers
- Our code will auto scale when needed
- We will pay only when the code is running (when there are no customers - this service is free)
- Very easy to deploy new versions, and no downtimes
- Built-in monitoring with [cloudwatch](https://aws.amazon.com/cloudwatch/)

## Lambda cons
- Not ideal for 'customer facing' service because there is still latency issue on execution time.
- Locked into specific OS and Node version.
- Works on a black box - if something went wrong it's hard to understand what happened.
- The local environment can't be exact like Lambda.

## Summery
AWS lambda functions have some disadvantages (mostly latency issues)- but I personally think this kind of services will be the future of code deployments, and you should give it a try and test it by yourself.


