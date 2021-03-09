# Introduction to Classic Load Balancers

## Cloud Service Provider
* Amazon Web Services (AWS)

## Difficulty
Introductory

## Scenario
Demonstrate using Classic Load Balancers by distributing traffic between 2-3 different EC2 instances.

A Classic Load Balancer is an old generation load balancer that supports HTTP/HTTPS(layer 7) and TCP(layer 4). They also have "aesthetic host names", whereas NLB's have "aesthetic IP's". It's recommended to utilize the newer load balancers, but for the sake of practicing, let's do it!

###  Complete the following:

* Task 1: Configure an EC2 instance that has an Apache HTTP server installed on it -- to display a simple webpage.
  1. Create 2-3 EC2 all in different AZ.
  2. Login SSH through terminal.
  3. Enter the following:
      sudo su
      yum update -y 
      yum install -y httpd.x86_64
      clear
      systemctl start httpd.service
      systemctl enable httpd.service
      curl localhost:80   -- *curl: used to load whatever is in the URL
  
  **How do we access the website in the browser instead of the terminal?**
  4. Change inbound rules in security for our instances to allow port 80
  5. Enter the following in the browser:
      https://<IP_Address>
  6. Congradulations you have access to the Test Page!
  7. Try adding content through the terminal.
  8. Enter the following into the terminal:
      echo "Hello World" > /var/www/html/index.html
      echo "Hello World from $(hostname -f)" > /var/www/html/index.html
  9. Test this entering **hostname -f**, [this]() should be outputed.

* Task 2: Create a CLB.
  1. Scroll down and click **Load Balancers**
  2. Select **Classic** and name the CLB "CLBPractice"
  3. Creating an internal balancer means that we won't be able to access it, **don't enable**
  4. Continue to **Assign Security Groups**
  5. Create a new security group and name "my-first-load-balancer"
  6. *Notice how we are not using the same security group as the instance we are connecting to
  7. Ignore warning and continue.
  8. **Check:** enter **<ip>/index.html**, output should say "Hello World"
  9. 

* Task 3: Edit inbound rules for Security Groups.

* Task 4: Test CLB.