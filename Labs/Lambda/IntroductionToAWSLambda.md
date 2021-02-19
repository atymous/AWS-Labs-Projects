# Introduction to AWS Lambda 

## Cloud Service Provider
* Amazon Web Services (AWS)

## Difficulty
Introductory

## Scenario
Demonstrate using Lambda by creating a serverless image thumbnail application.
  1. User will upload an *object* into a *source bucket*.
  2. Amazon S3 will detect the event and publishes the event to AWS Lambda. This occurs by invoking the Lambda
  function and transferring/passing the event data as a function parameter.
  3. Execution of the lambda function.
  4. Lambda function contains the source bucket name and object key name. AWS Lambda can now read the objects, can use the graphite libraries to create thumbnails, and save those thumbnails to the *target bucket*.

Refer to this [image](https://github.com/atymous/AWS-Labs-Projects/blob/master/Labs/Lambda/IntroLambdaScenario.png)

###  Complete the following:

* step1


###  Questions to think about 

* ???


## References 
* [QwikLabs](https://www.qwiklabs.com/focuses/15682?catalog_rank=%7B%22rank%22%3A2%2C%22num_filters%22%3A3%2C%22has_search%22%3Atrue%7D&parent=catalog&search_id=8999985)