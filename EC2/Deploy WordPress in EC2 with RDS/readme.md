**Step 1: Creating a MySQL Database with Amazon RDS**

1.	Goto RDS and start creating a database with Standard create method.
2.	Select MySQL database engine and its version and select the Free tier template.
3.	In the Settings section, give name for the DB instance identifier.
4.	Then specify the master username and password for your database.
5.	Choose instance settings as required.
6.	Keep it in default VPC.
7.	Skip to the Additional Configuration section at the end of the page and expand it.
8.	Assign the Initial database name.
9.	Keep the rest of the settings as required.
10.	 Then click on create database.

     ![image](https://user-images.githubusercontent.com/73180656/214882296-a0615ffa-6783-428e-81d0-324f27ab66ae.png)

**Step 2: Create an EC2 Instance.**

1.	Use Amazon Linux AMI.
2.	And allow HTTP traffic in security group.
3.	Configure rest of the settings as required.

**Step 3: Configuring Amazon RDS Database.**

1.	Edit the Inbound rules of RDS security group.
2.	Change the Type property to MYSQL/Aurora, which will update the Protocol and Port range to the proper values.
3.	In the Source value select the security group of the EC2 instance we created in Step 2.
4.	This rule will allow MySQL access to any EC2 instance with that security group configured.

    ![image](https://user-images.githubusercontent.com/73180656/214882623-f3972170-c808-497e-9ec1-036301e9fc7e.png) 

5.	Then SSH into the EC2 instance and connect to the RDS database with the following command:
```
mysql -h [db_endpoint] -P 3306 -u [db_user] -p
```
6.	Enter the password of the user to connect to the RDS Instance.

**Step 4: Configuring WordPress on EC2.**

1.	To run WordPress, we need to run a web server on your EC2 instance.
2.	To install and run Apache on your EC2 instance, run the following command:
```
sudo yum install -y httpd
sudo service httpd start
```
3.	Now, we will download the WordPress software and set up the configuration.
4.	First, download and uncompress the software by running the following commands:
```
wget https://wordpress.org/latest.tar.gz
tar -xzf latest.tar.gz
```
5.	Change the directory to the WordPress directory and create a copy of the default config file using the following commands:
```cd wordpress
cp wp-config-sample.php wp-config.php
```
6.	Open the wp-config.php file using the nano editor.
```
nano wp-config.php
```
7.	Edit the database configuration by changing some things.
8.	The values should be:
```
DB_NAME: “<name_of_the_database>”
DB_USER: The name of the user you created in the database in the previous module.
DB_PASSWORD: The password for the user you created in the previous module.
DB_HOST: The hostname of the database that you found in the previous module.
```
9.	The second configuration section we need to configure is the Authentication Unique Keys and Salts. It looks as follows in the configuration file:

    ![image](https://user-images.githubusercontent.com/73180656/214883977-be1ea780-c1db-49f3-984b-11e6593ec74b.png)
    
10.	 Go to this link to generate values for this configuration section. Replace the entire content in that section with the content from the link. Save it.
11.	 Install the application dependencies needed for WordPress, copy the WordPress application files into /var/www/html directory used by Apache and Restart the Apache web server to pick up the changes.
```
sudo amazon-linux-extras install -y lamp-mariadb10.2-php7.2 php7.2
sudo cp -r wordpress/* /var/www/html/
sudo service httpd restart
sudo service httpd restart
```
14.	 Then go the Public IP address of the EC2 instance, we should see the WordPress welcome page and the five-minute installation process.

     ![image](https://user-images.githubusercontent.com/73180656/214884793-2d7b6d85-4802-4036-a9ad-dd4999bce92c.png) 

