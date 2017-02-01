# AWS lambda functions introduction

## What is AWS lambda anyway?
On 2015 Amazon introduces us [AWS Lambda functions](http://docs.aws.amazon.com/lambda/latest/dg/welcome.html) - a serverless compute platform for stateless code execution in response to triggers.


Basically - we split the code into small stateless functions (microservices) that execute in response to triggers. Those triggers can be:
- HTTP request to specific end -point
- File PUT event on s3 bucket
- AWS SDK event call
- New event on SQS (AWS queue system)


When using Lambda functions - we reduce significantly server maintenance complexability (no need to launch server instance, configure it, handle scaling, monitoring, security, versioning etc.).

Instead - all we need to do is to configure this functions with the AWS interface and deploy the code into it (just by uploading zip file).


Then continuing working on new features or improve current one’s, without worrying about all these infrastructure issues.

## How to use AWS lambda

 AWS gives us simple function signature with 3 parameters that look like that:
 
 ```javascript
 exports.handler = (event, context, callback) => {
    //event - the event that triggers this function
    //context - some data about the context this function run at
    //callback - to execute when we want to resolve it.
    
    // write your logic here
 };
 ```
We only need to write our logic into this function. we can use any NPM package we want, and write our code like any other microservice on node environment (notice -lambda support many other [languages](http://docs.aws.amazon.com/lambda/latest/dg/current-supported-versions.html) - but this is out of the scope of this post).


## Usage example
Here is a simple example of Lambda function that triggered when someone put a PDF file on s3, and want to create a thumb out of it:

![pdf-to-thumb lambda function](http://rawdata.adicarmel.com.s3.amazonaws.com/tmp/lambda-pdf-to-thumb.png)


This function does the following:
- read the file path and name from the event (lines 7-8)
- goes to s3 bucket and retrieve this file (line 11)
- use 'gm' (a package that wraps 'image-magic' - a tool for image processing) to convert PDF to thumb PNG image (lines 15-18)
- upload the thumb PNG image back to s3 bucket (line 22)
- use 'context.done' to resolve the function with or without an error

And that's it! 

This code will be highly available and secured on AWS servers without the need to know how to set up and maintain servers.

## Lambda pros

- Our Code will be highly secured on AWS servers
- Our code will auto scale when needed
- We will Pay only when the code is running (when there are no customers - this service is free)
- Very easy way to deploy new versions, and no downtimes
- Built-in monitoring with [cloudwatch](https://aws.amazon.com/cloudwatch/)

## Lambda cons
- Not ideal for 'customer facing' service because there is still latency issue on execution time.
- Locked into specific OS and Node version.
- Works on a black box - if something went wrong it's hard to understand what happend.
- The local environment can't be exact like Lambda.

## Summery
AWS lambda functions have some disadvantages (mostly latency issues)- but I personally think this kind of services will be the future of code deployments, and you should give it a try and test it by yourself.

