# AWS lambda functions introduction

## What is AWS lambda anyway?
On 2015 Amazon introduces us [AWS Lambda functions](http://docs.aws.amazon.com/lambda/latest/dg/welcome.html) - a serverless compute platform for stateless code execution in response to triggers.


Basically - you can split your code into small stateless functions (microservices) that execute in response to triggers. Those triggers can be:
- HTTP request to specific end -point
- File PUT event on s3 bucket
- AWS SDK event call
- New event on SQS (AWS queue system)


When you use Lambda functions - you can reduce significantly server maintenance complexability (no need to launch server instance, configure it, handle scaling, monitoring, security, versioning etc.).

Instead - all you need to do is to configure this functions with the AWS interface and deploy your code into it (just upload zip file).


Then you can continue working on new features or improve your current one’s, without worrying about all these infrastructure issues.

## How to use AWS lambda

 AWS gives us simple function signature with 3 parameters that looks like that:
 
 ```javascript
 exports.handler = (event, context, callback) => {
    //event - the event that triggers this function
    //context - some data about the context this function run at
    //callback - to execute when we want to resolve it.
    
    // write your logic here
 };
 ```
We only need to write our logic into this function. we can use any NPM package we want, and write our code like any other microservice on node enviroment (notice -lambda support many other [languages](http://docs.aws.amazon.com/lambda/latest/dg/current-supported-versions.html) - but this is out of the scope of this post).


## Usage example
Here is a simple example of Lambda function that triggered when someone put a PDF file on s3, and want to create a thumb out of it:

![pdf-to-thumb lambda function](http://rawdata.adicarmel.com.s3.amazonaws.com/tmp/lambda-pdf-to-thumb.png)


This function does the following:
- read the file location from the event (lines 7-8)
- goes to s3 bucket and retrieve this file (line 11)
- use 'gm' (package that wraps 'image-magic' - a tool for image processing) to convert PDF to thumb PNG image (lines 15-18)
- upload the thumb PNG image back to s3 bucket (line 22)

And that's it! this code will be highly available and secured on AWS servers without the need to know how to setup and maintian servers.

## Lambda benefits

- Your code will be highly secured on AWS servers
- Your code will auto scale when needed
- You will Pay only when your code is running (if you still don't have customers - you won't pay anything)
- Very easy way to deploy new versions, and no downtimes
- Built-in monitoring with [cloudwatch](https://aws.amazon.com/cloudwatch/)

## Summery
AWS lambda functions have some disadvantages (mostly latency issues)- but I personally think this kind of services will be the future of code deployments, and you should give it a try and test it by yourself.

