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

## 1-7. Prepare the batch compute environment
* [Create a batch compute environment](https://console.aws.amazon.com/batch/home#/compute-environments)
* [Create a batch compute environment reference] https://docs.aws.amazon.com/batch/latest/userguide/create-compute-environment.html
* Modify serverless.yml at provider.environment.COMPUTE_ENVIRONMENT with the created batch compute environment name

## 1-8. Deploy
```
$ serverless deploy
```

# 2. 
## 
```
```