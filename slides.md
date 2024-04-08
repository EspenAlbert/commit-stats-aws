---
# try also 'default' to start simple
theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
# background: https://cover.sli.dev
# some information about your slides, markdown enabled
title: Commit Stats AWS UG
info: |
  ## From idea to product with AWS & Python
  Created with <3
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
# apply any unocss classes to the current slide
class: text-center
# https://sli.dev/custom/highlighters.html
highlighter: shiki
# https://sli.dev/guide/drawing
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations#slide-transitions
transition: slide-left
# enable MDC Syntax: https://sli.dev/guide/syntax#mdc-syntax
mdc: true
hideInToc: true
---

<!-- 
- About me
      - World map: Norway, Sweden, Spain, Thailand
      - Activities: Calisthenics, Weightlifting, sports
      - Career: Rocketfarm (consulting small team), wheel.me (startup), Smidige (contractor), and MongoDB (enterprise)
      - Tech choices: Python, Terraform, Pycharm -> VsCode, Golang, MongoDB, K8s+Istio, Markdown <3
      - Influencers: Cal (productivity & life philosophy), Podcasts (Latest tech news), Tim Ferriss+Lex Friedman (any life), Crossfit+ATG (exercise), Sam Harris (religion & meditation)
      - Dreams: Coworking Arinaga + Activity Center for Adults
  - Product:
    - Show sign up workflow and End Product
  - Architecture:
    - Don't expect you to understand but here it is: Figma
    - Go through the same steps
  - SaaS (non AWS):
    - MongoDB Atlas
    - InfluxDB Cloud
  - AWS Services & Lessons learned:
    - Route53
    - Cloudfront with edge Lambda
    - API Gateway
    - Lambda
    - S3
    - KMS
    - IAM
    - ECR
  - CI+CD?
    - Pants
    - Terraform CDK
  - Python Code
    - Pants build system
    - FastUI (FastAPI)
    - GitPython
    - model-lib
  - Golang CLI
    - Most useful with Toggl
  - Development history
    - Milestones
    - Detours
    - Cors Lesson
    - Where most my time went
  - Costs
    - AWS
    - SaaS
  - Future of the product
    - More robust onboarding experience
    - Open Source
    - See website
  - Questions? 
Quiz?
How many lambdas?
How much s3 storage?
How many AWS services?
How much money does this cost per month?
How many detours?
How many users?
How I got the job? 
Other tools?
Cors?
Terraform modules? 
Build time?
Testing? 

- Discussions
  - SPA, routing, staticfiles
    - FastUI
    - Lambda @ the edge
  - Guess how the application is deployed?
    - Build & Deployment tools
    - CDKTF
    - Other parts
  - AWS Lambda hosting size limitations & cold start
    - Show costs of provisioned and alternative for provisioning
  - SaaS & Database free tiers?
    - MongoDB
      - Flexible schema
      - Fast to test
      - Free
    - InfluxDB
      - Natural for timeseries
      - Free Tier (or not?)
  - Architecture diagrams?
  - Costs & cost monitoring & AWS multi account setup?
    - What is the most expensive part of this
  - Presentation tools:
    - [slidev](https://github.com/slidevjs/slidev)
-->

# From idea to product with AWS & Python

## Lessons learned from a two months hobby project

## AWS User Group 23rd of April

---

## Overview

<Toc v-click minDepth="1" maxDepth="1" mode="all"></Toc>


---

# Part 1: Commit Stats Product Demo
---
layout: two-cols
---

## About Me 1
- Geography
  - Born and raised in Kristiansand, Norway
  - Mom lives in Sweden
  - Thailand, Ko Lanta (Kohub)
  - ~4 years in Gran Canaria
  - Living with my fiancée Maria in Arinaga
- Activities: Calisthenics, Weightlifting, sports++
- Career:
  - Rocketfarm (consulting, small team)
  - wheel.me (startup)
  - Smidige (contractor)
  - MongoDB (enterprise)

::right::

![Arinaga](images/arinaga.png)

---

## About Me 2
- Tech choices:
  - Python
  - Terraform
  - Pycharm -> VsCode
  - Golang
  - MongoDB
  - K8s+Istio
  - Markdown <3
- Influenced by:
  - Cal (productivity & life philosophy)
  - Podcasts (Latest tech news)
  - Tim Ferriss+Lex Friedman (any life)
  - Health: Crossfit+ATG (exercise)


---

## Problem Statement

How do you show you can code if you have only worked in private git repos?

![no code 2021](images/no_code_2021.png)

![no code 2022](images/no_code_2022.png)

---

## Project Background (also found at the botton of [project landing page](https://commit-stats.ealbert.org/) )


I was applying for developer jobs and I couldn't show my coding experience.
The code repositories I had been working on were in different git providers (Gitlab & Azure DevOps) and the code was **private**.

As I am a bit of a data nerd 🤓 I like to track different metrics.
Not only commits, PRs, but also LoC (Lines of Code), open source contribution, 3rd-party packages, etc.
Therefore, the two main goals of the project are:

1. Support creating a "CV" page of your commit stats that you can use when applying for jobs
2. (Future) Support weekly feedback on your code and reflect on your developer journey

I hope you will find it useful and fun 😎
Happy coding!

---

## Product Demo 1

- "CV/Dashboard" of your commits across languages

![alt text](images/product_espen_cv.png)

---

## Product Demo 2

- How to collect the commits:

1. Login with Github
2. Add your token

![alt text](images/product_token_steps.png)

---

## Product Demo 3

- Select your repos
- Full Collection Status & Open Source Repos


![alt text](images/product_token_status.png)

---

## Product Demo 4

- Wait...
- Updated every 15 min

![alt text](images/product_wait.png)

---

## Product Demo 5

- Back to the beginning

![alt text](images/product_espen_cv.png)

---

## Architecture 😱

- [Figma](https://www.figma.com/file/sXDwzyzti2Q5TmNtpx7hmq/CommitStats?type=whiteboard&node-id=0-1)

![alt text](images/architecture.png)

---

## Future of the Project

- Alternative to InfluxDB for hosting
- Improved on-boarding experience
- [More in the `Future ideas` section](https://commit-stats.ealbert.org/)

---
layout: two-cols
---
# Part 2: Behind the scenes discussions

- Questions:
  1. How would you build this?
  2. Which AWS Services?
  3. Other SaaS products?
  4. Programming language?
  5. Commit to deployment workflow?
  6. Database technology?

<!-- 
::right::

<div class="mt-5">
</div>

### Overview

<Toc class="mt-5" v-click minDepth="2" maxDepth="2" mode="current"></Toc>
-->

---
layout: two-cols
---

## Tech stack decisions

- What stack would you choose?

<v-click>

- I'm a Python fan and inspired by Samuel Colvin starting the [pydantic company](https://github.com/pydantic)
  - [Pydantic Services Inc. emerges from stealth today with $4.7 million in seed funding led by Sequoia](https://techcrunch.com/2023/02/16/sequoia-backs-open-source-data-validation-framework-pydantic-to-commercialize-with-cloud-services/)
- Wanted to use [FastUI](https://github.com/pydantic/FastUI)
  - [7.1k stars in a few months](https://star-history.com/#pydantic/FastUI&Date)

<Transform :scale="0.75">

![alt text](images/fastUI_stars.png)

</Transform>

</v-click>

::right::

<v-click>

## Artifacts Produced

- classic static files
  - `index.css`
  - `index.html`
  - `index.js`
  - +++
- zip files for the lambda functions
- or a docker image

</v-click>
<v-click>

## Tech candidates

- Plotly Dash
- Your Choice?

</v-click>

---

## AWS Organization

- Would you use than more than one AWS account?

<v-click>

- Root account
  - Route53
  - IAM Config
  - ECR
- `{Project Name}` Account: CommitStats
  - Billing separate
  - Need access to route53 to add DNS records
- Terraform Basic Needs
  - S3 with replication
  - KMS (Optional -> can be costly)

</v-click>

---
layout: two-cols
---

## How to deploy the artifacts? Lambda/ECS/EC2?

- Artifacts reminder
  - Static files (index.css|html|js ++)
  - aws zip files
  - docker images?
- What would you choose and why?

<v-click>

- I chose Lambda

<Transform :scale="0.85">

![alt text](images/lambda_functions.png)

</Transform>
</v-click>

::right::


<Transform :scale="0.65">
<div class="ml-10">

<v-clicks>

- Why images? [250MB limit on Lambda functions](https://stackoverflow.com/questions/54632009/how-to-increase-the-maximum-size-of-the-aws-lambda-deployment-package-requesten)
  - Python packages 😱

  ```
  144M python3.11/site-packages//plotly
  89M python3.11/site-packages//pyarrow
  81M python3.11/site-packages//botocore
  71M python3.11/site-packages//pandas
  60M python3.11/site-packages//numpy
  42M python3.11/site-packages//dash
  ```

- How to choose memory size?
- How to trigger lambdas?
  - EventBridge (CloudWatch Events)
  - Supports schedule: `cron(0/15 ** *?*)` or `rate(1 minute)`
  - Specific event publishing by using `detail-type`, see `events.tf`
- Lambda cold start problem
  - [Provisioned concurrency](https://docs.aws.amazon.com/lambda/latest/dg/provisioned-concurrency.html) to the rescue? [redit thread](https://www.reddit.com/r/aws/comments/nh4nc0/aws_lambda_provisioned_concurrency_vs_keeping_a/)
  - 10 × 0.000004167 × 0.5 × 86400 = $1.80/day, or $54/month


</v-clicks>
</div>
</Transform>
---

## Staticfiles, CDN, APIs, CORS, and SPA how do you do the routing?

- Any suggestions?
- Fell on my face quite hard
  - Splitting the API into more services got complicated

---

## Database technology?
---

## Testing? Multiple environments? CI workflows?

- lambda versioning? aliases?

---

# Questions?


---

# Thank You

- AWS User Group organizers
  - Andrey
  - Antonio
  - Andras
- Leo for hosting us
- Everyone for joining
