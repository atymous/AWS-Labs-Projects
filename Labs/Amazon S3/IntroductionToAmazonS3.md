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
  2. Navigate to the S3 Management Console and add this file to your S3 bucket.
  3. Locate the Object URL for this file and notice that you are still denied access.
  4. Navigate to the IAM directory page and click **Roles**.
  5. Search for the field type **EC2InstanceProfile**
  6. On the Summary page, copy the **Role ARN** to a text file for later.
  7. Navigate to the S3 management console and select the bucket.
  8. Make sure there are both objects in the bucket.
  9. Choose the **Permissions** tab.
  10. Scroll down to the **Bucket Policy** and click **Edit**.
  11. Copy this [Bucket ARN] to a text file for later.
  12. Select **Policy generator** to create a bucket policy.
  13. Apply the AWS Policy below to the generator:
      Select Type of Policy:
      Effect:
      Principal:
      AWS Service: keep default setting of S3
      Actions: PutObject and GetObject
  14. Select **Add Statement** and then **Generate Policy**. (Should look similar to [this])
  15. Copy/paste this policy into the **Bucket policy editor**.
  16. Save changes.
  17. Navigate back to the SSM window.
  18. Enter the following:
      pwd
      output: /home/ssm-user/reports  (*where you would run your commands*)
      aws s3 ls s3://reportbucket11 (*command to list all objects in bucket*, seen [here])
      cd reports  (*change directories into the reports directory*)
      ls  (*command to list contents in directory*, seen [here])
      aws s3 cp report-test1.txt s3://reportbucket11 (returns the [following])
      aws s3 ls s3://reportbucket11  (see if the file is successfully uploaded to S3)
      aws s3 cp s3://reportbucket(NUM)/sample-file.txt sample-file.txt
      *above command retrieves(GetObject) a file from S3 TO THE EC2 instance*
      ls  (should now see the sample-file in the file list, output should resemble [this])
  19. Refresh the Object URL for the txt file. We are still denied access because the Bucket Policy only gave rights to the principle called **EC2InstanceProfielRole**.
  20. Go back to the Policy Generator and allow EVERYONE(*), Read access (GetObject).
  21. Test if this policy works on your own by refreshig the URL once again.
  22. Leave the tab with the sample-file.trxt for later.

* Task 6: Explore Versioning
  1. Navigate to the Bucket overview page
  2. 



###  Questions to think about 
* What does Amazon S3 buckets store?

* State one reason why the Object URL would result with an **Access Denied** error. [Task 3]

* What is the default for Amazon S3 security? [Task 3]

* Can everyone have access to the objects inside of the S3 bucket? [Task 3]
  Because the Session Manager uses HTTPS port 332, there is no need for us to open SSH port 22 to the outside world. Think of it as the terminal that we can access through the Cloud.

* How can we get public access for all our objects in our S3 bucket. [Task 5]
  By configuring a *bucket policy* to grant access to all objects in the bucket without the need to specify permissions on each object individually. 

* What is the **EC2InstanceProfileRole** responsible for? [Task 5]
  This is the Role that the EC2 instance uses to connect to Amazon S3.

* What are ARN's? (Amazon Resource Names)
  They uniquely identify AWWS resources across all of AWS

* What does "versioning" mean? [Task 6]
  Versioning refers to a way of keeping multiple variants of an object in the same bucket. Versioning can be used to preserve, retrieve, and restore every version of every object stored in your S3 bucket. Versioning can also be used to easily recover from both unintended usesr actions and application failures.

### Learning Outcome


## References 
* [QwikLabs](https://www.qwiklabs.com/focuses/16438?catalog_rank=%7B%22rank%22%3A4%2C%22num_filters%22%3A0%2C%22has_search%22%3Atrue%7D&parent=catalog&search_id=9162506)