Steps to host a website in EC2 (Linux) in AWS.
1.	First, we need an EC2 instance to host our website.
2.	Choose Amazon Linux 2 Image when creating an EC2 instance.

    ![image](https://user-images.githubusercontent.com/73180656/214860692-45649ce0-9317-429f-a4c6-bdc02ff1cbe8.png)

3.	Allow ssh and http connections during configuration settings and keep everything else as needed.
4.	Before launching the instance create a bucket in s3 and put an index.html file in it.
5.	Also make sure the bucket and the html file in it is public.
6.	EC2 will to get the code from S3 bucket. So, create IAM Role to give EC2 permission to access S3.
7.	Goto IAM and create a new role of s3FullAccess.
8.	After creating this role attach it to the EC2 instance that was just created.
9.	Now, launch the machine and connect it using ssh.
```
ssh -i "private key file" <username>@public_ip_of_instance
```
10.	 After login in the machine follow the bellow commands to install LAMP web server.
  
    sudo yum update -y
    sudo amazon-linux-extras install -y lamp-mariadb10.2-php7.2 php7.2
    sudo yum install -y httpd mariadb-server

11.	 Start the Apache web server.
 
    sudo systemctl start httpd
    sudo systemctl enable httpd 
  

12.	Now, copy content of website from S3 to directory /var/www/html in EC2. Make sure to change S3 bucket name.
```
sudo aws s3 cp s3://<bucket name> --region <region name> /var/www/html/ --recursive
```
13.	 It’s done, now go to the public IP of the EC2 instance.

     ![image](https://user-images.githubusercontent.com/73180656/214864635-2cd4736b-9b1a-4ec4-b626-0128b624f158.png)

  
