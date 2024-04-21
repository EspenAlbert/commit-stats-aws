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
  - Family in Stockholm, Sweden and siblings in Oslo, Norway
  - 3rd home in Ko Lanta (Kohub), Thailand
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
  - Tim Ferriss+Lex Friedman (Exposure to different thinkers)
  - Health: Crossfit+ATG (exercise)
- More info [at my Github page](https://github.com/EspenAlbert)

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

- ["CV/Dashboard" of your commits across languages](https://commit-stats.ealbert.org/cv/EspenAlbert)

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

- Questions we will touch on:
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

  - ECR Lifecycle rules

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
<v-click>

- Fell on my face quite hard
  - Splitting the API into more services got complicated
  - CORS (Cross Origin Resource Sharing)
    - Where to add the headers?

</v-click>

---
layout: image
image: ./images/routing.png
backgroundSize: contain
---
<div class="ml-8">

## My Solution


<Transform :scale="0.65">

### Cloudfront

<v-clicks>

- [AWS WAF](https://us-east-1.console.aws.amazon.com/wafv2/homev2/start?region=us-east-1)? No
  - Minimum price of 5$ + 1$ per rule
- SSL/TLS managed by AWS
- Origins
  - HTTP -> HTTPS redirect
  - Choose caching behavior
    - Managed-CachingOptimized
    - Managed-CachingDisabled
  - Choose Response headers policy
    - Managed-AllViewerExceptHostHeader (believe due to gateway routing)
    - Managed-CORS-CustomOrigin
- Can hook into the request stages with Function associations
  - CloudFront Functions?
  - [Lambda@Edge](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/lambda-edge-how-it-works.html)
  - Hook points

</v-clicks>

<Transform :scale="0.65" class="ml-8">

<v-click>

![cloudfront](images/cloudfront.png)

</v-click>

</Transform>


</Transform>

</div>

<!-- 
1. Start by explaining the overall view
2. Talk about cloudfront (click next)
3. Can use the tools in chrome to inspect the network calls to see the hits
-->

---
layout: image
image: ./images/routing_lambda.png
backgroundSize: contain
---

<div class="ml-8">

#### Lambda @ Edge

<v-click>

```python{all|7-10|1-3,11-13|14-}
ALL_S3_DOCUMENTS = set(['CodeLazy.js', 'CodeLazy.js.map', 'MarkdownLazy.js', 
'MarkdownLazy.js.map', 'index.css', 'index.html', 
'index.js', 'index.js.map'])

def lambda_handler(event, context) -> dict | None:
    """based on example: https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/lambda-examples.html#lambda-examples-redirect-to-signin-page"""
    request: dict = event["Records"][0]["cf"]["request"]
    path = request["uri"]
    print(f"path is: {path}")
    s3_path = path.lstrip("/")
    if s3_path in ALL_S3_DOCUMENTS:
        print(f"no redirection {s3_path} exist")
        return request
    print("returning html directly")
    return {
        "status": "200",
        "statusDescription": "OK",
        "body": _html,
        "bodyEncoding": "text",
        "headers": {
            "content-type": [
                {
                    "value": "text/html;charset=UTF-8",
                }
            ]
        },
    }
```

</v-click>

</div>

---

- inside of python script: `_html=`

```html{all|6|7-8}
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>CommitStats Landing Page</title>
    <script type="module" crossorigin src="/index.js"></script>
    <link rel="stylesheet" crossorigin href="/index.css">
  </head>
  <body>
    <div id="root" class="highcharts-light"></div>
  </body>
</html>
```

---

## AWS Gateway

- [AWS API Gateway](https://eu-west-1.console.aws.amazon.com/apigateway/main/develop/routes?api=gjwn13z2g8&integration=rnf8hmg&region=eu-west-1&routes=qls5ftn)
- Anyone experience with multiple stages?

---

## Database technology?

<v-clicks>

1. [MongoDB Atlas with Free Forever (up to 512MB)](https://www.mongodb.com/pricing)
   1. Use AWS KMS to encrypt the tokens
2. [InfluxDB Cloud Serverless ($250 in free credits for 90 days)](https://www.influxdata.com/influxdb-pricing/)

</v-clicks>

<v-click class="mt-5">

- What DB are you using?

</v-click>

---

## Cost of the solution?

<v-clicks>

- Which AWS service do you think is the most expensive?
- KMS
  - Stopped encrypting terraform state to save money
- [Cost Explorer](https://us-east-1.console.aws.amazon.com/costmanagement/home?region=eu-west-1#/cost-explorer?chartStyle=STACK&costAggregate=unBlendedCost&endDate=2024-03-31&excludeForecasting=false&filter=%5B%5D&futureRelativeRange=CUSTOM&granularity=Monthly&groupBy=%5B%22Service%22%5D&historicalRelativeRange=LAST_6_MONTHS&isDefault=true&reportName=New%20cost%20and%20usage%20report&showOnlyUncategorized=false&showOnlyUntagged=false&startDate=2023-10-01&usageAggregate=undefined&useNormalizedUnits=false)
- InfluxDB, most costly for now ($2.49 for February)
  - Data out $0.17 for 1.88GB
  - Data In $1.59 for 635.851 MB
  - Query count $0.64 for 5342 queries (0.012 per 100 query executions)
  - Storage:$0.09 for 43.461 GB-hr

</v-clicks>

---

## Multiple environments? CI workflows?

- What if you need to host stage/QA environments?
- Recreate the full terraform with a new environment or re-use infrastructure
- lambda versioning? aliases?
- TF code walkthrough?

---

## Quality checks & Local testing

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
- [slidev](https://github.com/slidevjs/slidev)
