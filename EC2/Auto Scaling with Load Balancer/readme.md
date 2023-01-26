**Here we will host a website on EC2 and configure it for Auto Scaling using Load Balancer. It will allocate and deallocate resources as per requirements.**

1.	First, create a Launch Template in which we will describe the resources to launch when needed.
2.	Goto Launch Template under Instances tab in EC2.
3.	Start creating a launch template.
4.	Give name of the template, select AMI, instance type, key pair login, create a new security group with HTTP access allow for all Ips.
5.	Expand Advanced details tab and give IAM role of s3 full access.
6.	In the User data box at the end of the page add the following lines:
```
#!/bin/bash
sudo yum install httpd -y
sudo service httpd start
sudo chkconfig httpd on

sudo aws s3 cp s3://<bucket name>/<folder name> --region <region name> /var/www/html/ --recursive
```
7.	Keep everything else default if not needed.

    ![image](https://user-images.githubusercontent.com/73180656/214880948-6a1ac362-c17e-45d8-b73e-d74b8c5c6a70.png)

8.	Now, create a target group for the instances that will be created.
9.	Goto target group under load balancing.
10.	 Start creating it.
11.	 Choose target type as instances, give target name, select default vpc, protocol version HTTP1, select health check protocol as HTTP and give default path ‘/’ in health check path.
12.	 Click on next and don’t add targets and create target group.

     ![image](https://user-images.githubusercontent.com/73180656/214881179-8f69cd85-90fd-496e-a9d2-79e52fb93b3b.png)

13.	 Now we will create Load Balancer for our website.
14.	 Start creating an Application Load Balancer.
15.	 Give name of Load balancer, keep default VPC and select at least 2 subnets.
16.	 In listeners and routing, forward HTTP port traffic to the target group we just created.
17.	 Keep everything else as default.

     ![image](https://user-images.githubusercontent.com/73180656/214881260-673267a1-302c-4f90-ba92-4a62fd5cd7b7.png)

18.	 After creating Load Balancer, we will create Auto Scaling group.
19.	 Give name and assign Launch Template we created before.
20.	 Then select default VPC and 2 subnets from that VPC.
21.	 Then select Attach to an existing load balancer and select target group and select heath grace period as required.
22.	 In group size assign Desired, minimum and maximum capacity of instances for auto scaling.
23.	 Then select target scaling policies and give metrics for the auto scaling process.
24.	 Then we can give notification topic for all the processes that will take place during auto scaling.
25.	 Keep everything else default and create it.

     ![image](https://user-images.githubusercontent.com/73180656/214881351-73128557-ff94-4155-82b0-bb3e4fbe2847.png)

26.	 It’s done now go to load balancer and copy the DNS name from the description of that load balancer and paste it in the browser, it will open the website we hosted in EC2.
27.	 To check the auto scaling we can manually shut down httpd service in the instance and new instance will be created automatically.
28.	 Also, we can stress test our website using the following commands.
```
sudo amazon-linux-extras install epel -y
sudo yum install stress -y
stress --cpu 8 --timeout 3000
```
29.	 Wait for 5 mins to see the scaling activities.
