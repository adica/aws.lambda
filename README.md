# aws.lambda

As full-stack developers, we need to sharpen our skills in many languages and techniques both on client and server side.


In addition - these days, to be a great developer it’s not enough, you also need to know how to deploy your code right.


In AWS environment you need to learn how to:
- Launch [EC2 instance](https://aws.amazon.com/ec2/)
- Configure this instance (decide the amount of memory, disk space, CPU etc.)
- Deploy your code on it
- Monitor your app and determine when there are issues and fix them
- Handle your application scaling by yourself
- Manage new versions strategy (downtime handling)


Another option is to use “[AWS Elastic Beanstalk](https://docs.aws.amazon.com/console/elasticbeanstalk/get-started)” or “[AWS ECS](http://docs.aws.amazon.com/AmazonECS/latest/developerguide/ECS_GetStarted.html)” (if you are using Docker).


Anyway you will choose - you will need to “fight” the machines, learn more techniques and maintain your  server/s from now on - and all you ever wanted was to show your application to the world...


On 2015 AWS introduce us [Lambda functions](http://docs.aws.amazon.com/lambda/latest/dg/welcome.html) - a serverless compute platform for stateless code execution in response to triggers.


Basically - you can split your code into small stateless functions that execute in response to triggers. Those triggers can be:
- HTTP request to specific end -point
- File PUT event on s3 bucket
- AWS SDK event call
- New event on SQS (AWS queue system)


When you use Lambda functions - you can reduce significantly server maintenance complexability.
All you need to do is to configure your lambda functions with the AWS interface and deploy your code into it (just upload zip file).


Then you can continue working on new features or improve your current one’s, without worrying about all these infrastructure issues.


From now on you will enjoy those features:
- Your code will be highly secured on AWS servers
- Your code will auto scale when needed
- Your code will run only when needed
- You will Pay only when your code is running (if you still don't have customers - you won't pay anything)
- Very easy way deployment of new versions
- Built-in monitoring with [cloudwatch](https://aws.amazon.com/cloudwatch/)
- No downtime when deploying new versions


AWS lambda functions have some disadvantages - but I personally think this kind of services will be the future of code deployments, and  you should give it a try and test it by yourself.

