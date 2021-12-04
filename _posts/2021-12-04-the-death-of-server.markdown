---
layout: post
title:  "Serverless: The Death Of Server"
date:   2021-12-04 14:58:00 -0300
categories: serverless aws cloud
---


Software development every year gains a lot of buzz words and one of them is serverless. Since it is released in 2014 by Amazon Web Services(AWS), grow every day your adoption in various companies around the world, to be a productive approach to develop applications.
Serverless has been a trending topic in the software development community in the last few years. As you can see in the image below the search term on Google increased as microservices over the years.

>Legend: The red is microservices and blue is serverless
![google-trands](/assets/google-trands.png)
>source: https://trends.google.com/trends/explore?date=all&q=serverless,microservices

This new approach to develop release software is more cloud native than others, to abstract the infrastructure from developers. But, to fully understand how we come in serverless, we need a sneak peek into the past as the evolution of release software changes.
Probably most of us work in a company that has its infrastructure like data centers with physical servers and the entire operation to buy, change, discard the server is the responsibility of the IT operations department, as if upgrade the OS System, install security patches and so on. Maintaining the own data center is very expensive and the cost of the equipment along the time is deprecated.

>Legend: The red is microservices and blue is serverless
![google-trands](/assets/google-trands.png)
>source: https://trends.google.com/trends/explore?date=all&q=serverless,microservices

After the on-site era, appear the Infrastructure as a Service(IaaS), where everything in the above of SO is transparent for us, our operations systems don’t care about it.
Following in the evolution time we have Platform as a Service(PaaS), where the level of the infrastructure abstraction is interesting for a team that does not have high skill in operations or we do not have the capacity or the time to market is so narrow. In this approach, the development team focuses on the applications and delivers value to customers faster.
And finally, the last model of infrastructure is the Software as a Service(SaaS), that are so popular today, because is more easy contract third-party software and plugin on our infrastructure than building from scratch. And another reason for it is to focus on our business domain. Imagine a ecommerce that needs to have a fraud prevention system, maybe its core domain is the sales of goods and the company could contract a respected vendor to use your fraud detection tool. Wherever the company teams focus on core business.
The image below shows the perspective of who manages the infrastructure.


![cloud-computing](/assets/cloud-computing-evolution.png)
>source: https://www.redhat.com/pt-br/topics/cloud-computing/iaas-vs-paas-vs-saas

The image below shows the perspective of cloud computing evolution.

![cloud-evolution](/assets/cloud-evolution.png)
>source: https://docs.microsoft.com/en-us/dotnet/architecture/serverless/

Serverless architecture, serverless computing, or function as a service(FaaS) are similar terms for Serverless that you can see in the industry. As you can imagine the main characteristic of Serverless is to be an approach without management of infrastructure, the own name means without server or less server from the perspective of the customer of the service.
Serverless is best for short-lived processes without predictable traffic, the instance of function has a limit to executing and when it is inactive for some time, the cloud provider terminates the instance. And, when we think about this approach, we should build a stateless process.

<br />


# Why
- Focus on product development by the team, because without a server to manage and operate, the developers could care about the business requirement that should resolve a real problem.
- Reduction of the infrastructure cost, Serverless you pay what you use, never for idle capacity as an EC2 instance or the total cost on-site.
- The responsibility to scale the service is from your cloud provider, when the application receives heavy traffic, the cloud provider allocates more instances of lambdas to treat the requests. And most importantly, you have a great time of operations behind the AWS for example, if you use it.
- Availability is another benefit in serverless, one more time, here we have the expertise of the cloud provider engineers to take care of the infrastructure, and the lambda executes across multiple availability zones in a region.
- We can have a reduction in the time to market when the developers only focus on the business problem.

<br />

# Why not
- Applications with long-running life cycle, stable or predictable workloads is not good to use.
Platform dependency, the code that you write in a particular cloud provider only works there, you are vendor lock-in. But, there are frameworks in the community that abstract what cloud do you use. Another aspect of the dependency is perhaps your cloud provider goes down in one region that your application is hosted or has instability you should switch to another region or wait until the services are reestablished.
- Could starts in the first or after a period inactivity could be a problem for your business if you need always respond to the entire request in the low latency. Imagine a financial trading application where milliseconds is very important to earn money o loss.
- Debugging, monitoring, and tracing in serverless can be difficult.
Integration tests can be challenged without a serverless framework.
- Limit of concurrent execution per region.

<br />


# The anatomy of AWS Lambda

The primary serverless provider was AWS lambda launched in 2014, and today AWS is the most used cloud provider by market share. Let's analyze your running.

![lambda-lifecycle](/assets/aws_lambda_cold_start.png)

Cold start is the time that your function takes to be ready to process the first request. When you deploy your code on AWS the package is downloaded from the S3 bucket, unzipped, and executed by the platform, and when your application is started is called warm start.
The cold start happens once a time after the first initialization or whether an application is terminated after an idle period of time of about 5 minutes, but it is not precise.
The image below shows the life cycle of requests along the time with a cold and warm start.

![lambda-simultaneous-requests](/assets/cold-start-simultaneous-requests.png)
> source: https://aws.amazon.com/blogs/compute/operating-lambda-performance-optimization-part-1/

And after it's warm.

![lambda-lifecycle](/assets/warm-start-requests.png)
> source: https://aws.amazon.com/blogs/compute/operating-lambda-performance-optimization-part-1/


AWS offers concurrent provisioning that keeps some lambdas warmed to the first requests, but it has a cost. The image below shows it, only invocation duration is counted in the response time.

![lambda-lifecycle](/assets/provisioned-concurrency.png)
> source: https://aws.amazon.com/blogs/compute/operating-lambda-performance-optimization-part-1/


The choice of the programming language impacts a cold start, compiled languages like Java are slower to execute, instead of interpreted languages like Python. The size of the package could impact the cold start too.

![lambda-benchmark-cold-starts](/assets/benchmark-cold-starts.png)
> source: https://mikhail.io/serverless/coldstarts/aws/

On AWS Lambda the only way to scale vertically is increasing the memory allocated to the lambda, which consequently bound more CPU to our serverless application, and one more time this cost money. The next image shows it for us.

![lambda-memory](/assets/lambda-memory.png)
> source: https://aws.amazon.com/blogs/compute/operating-lambda-performance-optimization-part-2/


And another way to improve performance on serverless applications is initializing heavy processes like a connection with a database out of the handler method of the function. Because the connection is open one time.

The image below shows a use case of serverless on AWS.

![lambda-lifecycle](/assets/web-app-example.png)
> source: https://aws.amazon.com/lambda/

The lambda is triggered by an event, that could be an API Gateway call, a message queue on SQS, a file on an S3 bucket, and so on.

<br />

# Vendor lock-in
To solve the issue of vendor lock-in appear some frameworks to help us do not to stay coupled with the cloud provider. Your use is important whether the strategy of the company is to be free to switch from one to another provider, of course, that is hard to happen when our company has an advantage contract with the cloud provider. But, as software engineers, we need to think about how to have low coupled in your architecture, and maybe one day save money with a contract more advantage to the company with another cloud provider with minimum change on your architecture.
Personally, I tested a framework called [Serverless Framework](https://www.serverless.com/framework/), it is easy to use and very productive, you could configure a simple lambda very fast with an API gateway, and your configurations are based upon the YAML file. Another nice feature is to run your function locally.
However, if your company runs its infrastructure over Kubernetes, no problem, you can use a solution called [Knative](https://knative.dev/docs/), it is like a plugin that is installed in the Kubernetes. And, today Kubernetes is a standard to deploy and manage containers in production, so don’t worry, probably anyone cloud provider has its solution to run Kubernetes.

<br />

# Serverless Databases
AWS developed the Aurora Serverless, a cloud-native database with MySQL compatibility. The characteristics are the same in terms of cost, you puy what you use only, we can develop an entire cloud-native application at low cost. The management is full of AWS.

<br />

# Summary
Serverless application is a buzzword today, but this approach of building application is so useful and interesting mainly to startups that are growing or in your discovery product and need delivery a high availability, elasticity, and reliable application without acknowledgment about infrastructure or simply because don't have time to spend with it. Using serverless applications we gain productivity in the initial stage and it could be a differential in the market capital today.


<br />

# Bibliography
[https://pkerrison.medium.com/pizza-as-a-service-2-0-5085cd4c365e](https://pkerrison.medium.com/pizza-as-a-service-2-0-5085cd4c365e)

[https://medium.com/thundra/getting-it-right-between-ec2-fargate-and-lambda-bb42220b8c79](https://medium.com/thundra/getting-it-right-between-ec2-fargate-and-lambda-bb42220b8c79)

[https://aws.amazon.com/blogs/compute/building-well-architected-serverless-applications-optimizing-application-performance-part-1/](https://aws.amazon.com/blogs/compute/building-well-architected-serverless-applications-optimizing-application-performance-part-1/)

[https://quintagroup.com/blog/aws-lambda-provisioned-concurrency](https://quintagroup.com/blog/aws-lambda-provisioned-concurrency)

[https://aws.amazon.com/blogs/compute/operating-lambda-performance-optimization-part-1/](https://aws.amazon.com/blogs/compute/operating-lambda-performance-optimization-part-1/)

[https://aws.amazon.com/blogs/compute/operating-lambda-performance-optimization-part-2/](https://aws.amazon.com/blogs/compute/operating-lambda-performance-optimization-part-2/)

[https://mikhail.io/serverless/coldstarts/aws/](https://mikhail.io/serverless/coldstarts/aws/)

[https://www.youtube.com/watch?v=Mz-b-rQ9wL0&list=PLEx5khR4g7PJNproQQ4SZ96Qeu-kr-Xbn&index=4](https://www.youtube.com/watch?v=Mz-b-rQ9wL0&list=PLEx5khR4g7PJNproQQ4SZ96Qeu-kr-Xbn&index=4)
















