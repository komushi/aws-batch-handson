# Tutorial I. Standard AWS Batch with custom array feature

# 1. Preparation
## 1-1. Check Node version
:warning: Make sure you have Node v8.x.x or v9.x.x:
:warning: Make sure you have Python 3.6.x:

```
$ node -v

$ python -V
```

## 1-2. Install serverless framework
```
$ npm install serverless -g
```

## 1-3. Get the hands-on source code
```
$ git clone https://github.com/komushi/aws-batch-handson
```

## 1-4. Install serverless plugins - only for development environment
```
$ cd aws-batch-handson/serverless-youtube-dl
$ npm install
```

## 1-5. Install python libraries
```
$ pip install -t vendored/ -r requirements.txt
```

## 1-6. Prepare the S3 bucket
* [Create an S3 bucket to batch results](https://s3.console.aws.amazon.com/s3/home)
* [Create an S3 bucket reference](https://docs.aws.amazon.com/AmazonS3/latest/gsg/CreatingABucket.html)
* Modify serverless.yml at provider.environment.YOUTUBE_DESTINATION_BUCKET with the created S3 bucket name

## 1-7. Prepare the Batch Compute Environment
* [Create a Batch Compute Environment](https://console.aws.amazon.com/batch/home#/compute-environments)
* [Create a batch compute environment reference](https://docs.aws.amazon.com/batch/latest/userguide/create-compute-environment.html)
* Modify serverless.yml at provider.environment.COMPUTE_ENVIRONMENT with the created Batch Compute Environment name

## 1-8. Deploy
```
$ serverless deploy
```

# 2. Test batch job - On-demand through API Gateway
## 2-1. Pick your favorite public playlist and invoke the API 
```
curl -X POST https://<your-api-key>.execute-api.<your-region>.amazonaws.com/dev/youtube-dl -d '{"url":"https://www.youtube.com/playlist?list=PLxeJ9A111coroEJyNYTrR7BR2_pY16_Kv"}'
```

## 2-2. Check the execution status
* [AWS Batch Dashboard](https://console.aws.amazon.com/batch/home#/dashboard)
* [AWS Step Functions
 State Machines Dashboard](https://console.aws.amazon.com/states/home#/statemachines)

# 3. Test batch job - On-demand through Step Functions Console Management
## 3-1. Open [AWS Step Functions State Machine Dashboard](https://console.aws.amazon.com/states/home#/statemachines)

## 3-2. Click the State Machine named 'youtube-dl'

## 3-3. Click the button 'Start execution'
* Pick your favorite public playlist and fill 'Input'
```
{"url":"https://www.youtube.com/playlist?list=PLxeJ9A111coroEJyNYTrR7BR2_pY16_Kv"}
```
* Click 'Start execution'

## 3-4. Check the execution status
* [AWS Batch Dashboard](https://console.aws.amazon.com/batch/home#/dashboard)
* [AWS Step Functions
 State Machines Dashboard](https://console.aws.amazon.com/states/home#/statemachines)

# 4. Test batch job - Scheduled Job by Cloudwatch event
## 4-1. Edit serverless-youtube-dl/serverless.yml
```
stepFunctions:
  stateMachines:
    YoutubeDownload:
      name: youtube-dl
      events:
        - http:
            path: youtube-dl
            method: post
        - schedule:
            rate: rate(5 minutes)
            enabled: true
            input:
              url: https://www.youtube.com/playlist?list=PLxeJ9A111coroEJyNYTrR7BR2_pY16_Kv
```

## 4-2. Deploy - under the folder 'serverless-youtube-dl'
```
$ serverless deploy
```

## 4-3. Check the execution status
* [AWS Batch Dashboard](https://console.aws.amazon.com/batch/home#/dashboard)
* [AWS Step Functions
 State Machines Dashboard](https://console.aws.amazon.com/states/home#/statemachines)
* [AWS CloudWatch Rules](https://console.aws.amazon.com/cloudwatch/home#rules:)

# 5. Clean-up - under the folder 'serverless-youtube-dl'
## 5-1. Remove the stack
```
$ serverless remove
```

## 5-2. Remove the S3 bucket

## 5-3. Remove the Batch Compute Environment