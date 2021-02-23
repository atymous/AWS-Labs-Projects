# Introduction to AWS Lambda 

## Cloud Service Provider
* Amazon Web Services (AWS)

## Difficulty
Introductory

## Scenario

You are working for a company utilizing Amazon S3 for data storage. Their application is residing on an EC2 instance and needs to push reporting data to an S3 bucket daily. Your task is to create an S3 bucket for your company to use for storing the report data. For a successful deployment, you must ensure that the EC2 instance has enough priviledges (*least priviledged principle*) to be able to upload and retrieve data from the S3 bucket. Files located inside the S3 buckets also require protection against accidental deletion. 

###  Complete the following:

* Task 1: Create a bucket
  1. Navigate to the S3 page and create a new bucket.
  2. In the General configuration section, name your bucket **reportbucket(NUMBER)**
    ex: reportbucket11

* Task 2: Upload an object to the bucket 
  1. Use and download this [image]() into your S3 bucket


* Task 3: Make an object public
**always test the bucket and object settings for security**
  1. In the report bucket located the object(image).
  2. Locate the **Object overview** section and copy the **Object URL** link.
  3. Open a new tab and copy/paste the URL link. Notice that there is an **Access Denied** error
  4. Make Object URL public by selecting **Object actions**, make public, and exit.
  5. Navigate to the S3 bucket and choose the **Permissions** tab.
  6. Edit the bucket settings and deselect the **Block *all* public access**.
  7. Save change and confirm.
  8. Navigate to object in the S3 bucket and select **Object actions**.
  9. Select **Make public** (will need to enable) and exit.
  10. Try the Object URL again.

* Task4: Test connectivity from the EC2 instance
  1. Navigate to the EC2 Dashboard.
  2. Under the **Resources** section, select **Instances(running)**.
  3. In **Connect to instance** window, select **Session Manager** for **Connection Management**.
  4. Click **Connect** and a new window will appear.
  5. Enter the following:
    cd ~
    pwd
    output: /home/ssm-user  (*where you would run your commands*)
    aws s3 ls  (*command to list all of S3 buckets*, seen [ex])
    aws s3 ls s3://reportbucket11 (*command to list all objects in bucket*, seen [ex])
    cd reports  (*change directories into the reports directory*)
    ls  (*command to list contents in directory*, seen [here])
    aws s# cp report-test1.text s3://reportbucket11
  6. An error will appear indicating that we only have **read-only** rights to the buckets.
  7. We need to permissions to perform the **PutObjects** operation.

* Task 5: Create a bucket policy
  1. Save this [file].
  2. Navigate to the S3 Management Console
  


###  Questions to think about 
* What does Amazon S3 buckets store?

* State one reason why the Object URL would result with an **Access Denied** error. [Task 3]

* What is the default for Amazon S3 security? [Task 3]

* Can everyone have access to the objects inside of the S3 bucket? [Task 3]

* What is the window that appears when connecting EC2 instance?
  Because the Session Manager uses HTTPS port 332, there is no need for us to open SSH port 22 to the outside world. Think of it as the terminal that we can access through the Cloud.

### Learning Outcome


## References 
* [QwikLabs](https://www.qwiklabs.com/focuses/15683?parent=catalog)