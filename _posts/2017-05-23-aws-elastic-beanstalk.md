---
layout: post
published: true
title: The good and bad about Elastic Beanstalk
mathjax: false
featured: true
comments: false
headline: The thinking about AWS Elastic Beanstalk
categories: 
  - AWS
tags: devops, AWS, container
---

At [DevOps Zen](https://www.devopszen.com/), we are always working on the infrastructure migration, application performance optimisation, IT cost reduction for small and medium internet companies. We see some companies use Elastic Beanstalk managing their AWS production stack. This article explains a little bit about AWS Elastic Beanstalk.

> Are you managing your application production stack with Elastic Beanstalk or thinking to migrate to?

AWS Elastic Beanstalk helps people not familiar with VPC, CF and ELB, ASG, Multiple available zone High availabilities etc AWS defined management components get started with the advantage of AWS. It reduced the learning curve of AWS components, glue them together and provides the solution supports auto scaling, security, monitoring etc. 

For short, it provides a managed environment and the essential components for your web applications such as Wordpress, Drupal, etc.

If you have the scaling issues, then [Elastic Beanstalk](https://www.devopszen.com/aws-elastic-beanstalk) can be a quick solution.

## The cost of moving to AWS Elastic Beanstalk

Before taking the action, have to estimate the cost and gain of using AWS EB.

### Have to integration with the AWS EB SDK:

Elastic Beanstalk provides the integration SDK for most common languages such as PHP, Java, Python, Ruby, Go, .NET, Node.js;
If you use web containers such as Tomcat, Passenger, IIS, you can also easily integrate with Elastic Beanstalk;
Elastic Beanstalk even supports Dockers or Multiple Dockers in the same instance.

AWS EB defines the stack for your application such as Proxy, Application server, Language version, Linux image. It also provides you rolling deployment, Blue/green deployment without downtime.

The good thing is you only have to think about the application layers once migrated to AWS EB. You don't have to think about scaling, high available, RDS, domain etc.

The bad is all of these are provided in one box, it is difficult to define your own stack or optimise it. It is possible to create your own machine images AMI with packer, but AWS EB itself has the learning curve and everything are rely on the AWS platform. 

### Have to split static files and source codes:

It is very common to see developers adding more and more static files into the code base, especially if the application is a CMS or publishing system. When migrating to AWS EB, have to keep the code base as small as possible and store other files on S3 or other storage. Because the lifecycle of static files and source code bundle are different.

## AWS EB management:

You can manage AWS EB with the web interface or with CLI:

```
brew install awsebcli
```

```
eb
usage: eb (sub-commands ...) [options ...] {arguments ...}

Welcome to the Elastic Beanstalk Command Line Interface (EB CLI).
For more information on a specific command, type "eb {cmd} --help".

commands:
  abort        Cancels an environment update or deployment.
  appversion   Listing and managing application versions
  clone        Clones an environment.
  codesource   Configures the code source for the EB CLI to use by default.
  config       Modify an environment's configuration. Use subcommands to manage saved configurations.
  console      Opens the environment in the AWS Elastic Beanstalk Management Console.
  create       Creates a new environment.
  deploy       Deploys your source code to the environment.
  events       Gets recent events.
  health       Shows detailed environment health.
  init         Initializes your directory with the EB CLI. Creates the application.
  labs         Extra experimental commands.
  list         Lists all environments.
  local        Runs commands on your local machine.
  logs         Gets recent logs.
  open         Opens the application URL in a browser.
  platform     Commands for managing platforms.
  printenv     Shows the environment variables.
  restore      Restores a terminated environment.
  scale        Changes the number of running instances.
  setenv       Sets environment variables.
  ssh          Opens the SSH client to connect to an instance.
  status       Gets environment information and status.
  swap         Swaps two environment CNAMEs with each other.
  terminate    Terminates the environment.
  upgrade      Updates the environment to the most recent platform version.
  use          Sets default environment.

optional arguments:
  -h, --help            show this help message and exit
  --debug               toggle debug output
  --quiet               suppress all output
  -v, --verbose         toggle verbose output
  --profile PROFILE     use a specific profile from your credential file
  -r REGION, --region REGION
                        use a specific region
  --no-verify-ssl       do not verify AWS SSL certificates
  --version             show application/version info
```

## Monitoring system

There is a simple monitoring system in AWS EB. You can see the request number per minute, CPU usage of the cluster, HTTP request latency, inbound outbound traffic.

You can also setup alarm based on the monitoring charts.

## The potential problems or issues

We don't like surprise.

### No Persistent Storage

Just like other EC2 instance in ASG, each instance can be started up or shut down at any time based on load. Thus, the disk attached to the EC2 instance will also be destroyed when the instance shutting down.

Have to think about storing the files user uploaded on S3.

### Cross region traffic

AWS charges cross region traffic, you will see this unexpected cost if you are running the application cross regions.

### The problems AWS EB can not sort out, but maybe you expect

AWS EB can't help with the application layer such as application performance, frontend performance, cost efficiency.

If you have performance issue then think about migrate to AWS EB, have to rethink about it.

And since AWS EB provide a stander solution, it is not tuned by default, you might see the cost growth compare with your legacy IDC.


## References:

* https://www.packer.io/
* http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/concepts.platforms.html
* http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/tutorials.html
* http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/eb-cli3.html

