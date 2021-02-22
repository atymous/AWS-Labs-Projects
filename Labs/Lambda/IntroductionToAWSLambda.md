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

* Task1: Create Amazon S3 Buckets
  1. Navigate to Amazon S3 and switch to the new console navigation at the top of the screen.
  2. Create bucket and name as "images-*random_num*". ()
  3. Create another bucket for the output and name as "images-*same_rand_num*-resized".
  4. Test set-up by uploading [HappyFace.jpg]()
  5. Upload image into the bucket named "images-*random_num*".

* Task2: Create AWS Lambda Function
  1. Navigate to the Lambda page.
  2. Create function and select *Author from scratch*.
  3. Configure the following in the window function
    Function name:
    Runtime:
    Expand *Change default execution role*
    Existing role: Select *lambda-execution-role*
    [*Note: Select Python 3.7]
  4. Create function.
  5. Click **+Add trigger** and configure the following.
    Select a trigger: S3 
    Bucket: Select images bucket
    Event type: *All object create events*
    Recursion invocation: select "I acknowledge" box
  6. Scroll to the bottom and click **Add** and **Create-Thumbnail** located at top of diagram.
  7. Scroll down to the **Function code** section and configure the following.
    Click **Actions** menu
    Upload a file from Amazon S3
    Copy/Paste this link and click **Save**
  8. Edit the Runtime settings, for **Handler** enter: CreateThumbnail.handler
  9. Click **save**.
  10. Edit the **Basic settings**, for **Description** enter: Create a thumbnail-sized image
  12. Click **save**


* Task3: Test Your Function
  1. Click **Test**, then configure **Event template**: Amazonm S3 Put and **Event name**: Upload.
  2. Replace the **example-bucket** in both locations to the name of your image bucket("images-*random_num*") in your text editor.
  3. Replace **test/key** with the name of the object uploaded(HappyFace.jpg).
  4. Click **Create** and then **Test**.
  5. Click **Details** to observe information including execition duration, resources configured, maximum memory used, and the log output.

* Task4: Monitoring and Logging
  1. On the Lambda service page, click **Create-Thumbnail** function.
  2. Click **Monitoring** tab.
  3. Click **View logs in CloudWatch** and click the **Log Stream** that appears.
  4. Expand and observe the messages to view log message details.

###  Questions to think about 

* What is the difference between a *source bucket* and a *target bucket*? [Task 1]
* Does the Lambda service work for your region? If not, which region did you need to change it to? [Task 1]
* What are *Blueprints*? [Task 2]
* What are the **Memory** and **Timeout** settings? [Task 2]
* What is displayed on the graphs in the **Monitoring** tab of the Lambda function? [Task 4]
  **Invocations:**
  **Duration:**
  **Errors:**
  **Throttles:**
  **Iterator Age:**
* Where are Lambda functions retained? [Task 4]

### Learning Outcome
* Create an AWS Lambda Function
* Configure an S3 bucket as a *Lambda Event Source*
* Trigger the Lambda Function everytime an image is uploaded onto the S3 bucket
* Utilize Amazon CloudWatch Log to monitor the execution of the Lambda S3 function

## References 
* [QwikLabs](https://www.qwiklabs.com/focuses/15682?catalog_rank=%7B%22rank%22%3A2%2C%22num_filters%22%3A3%2C%22has_search%22%3Atrue%7D&parent=catalog&search_id=8999985)