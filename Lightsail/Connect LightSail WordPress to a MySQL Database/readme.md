**Connect LightSail WordPress to a MySQL Database**

1.	First, make a WordPress website in LightSail.
2.	Then make MySQL database in RDS and make it publicly accessible. Make sure that you allow the WordPress IP address in the security group of MySQL database.
3.	Now, connect the WordPress instance using SSH and enter the following command to transfer the WordPress files in MySQL database.
```
sudo mysqldump -u root --databases bitnami_wordpress --single-transaction --compress --order-by-primary -p$(cat /home/bitnami/bitnami_application_password) | sudo mysql -u <DbUserName> --host <DbEndpoint> --password
```
4.	At the prompt, enter the password for your MySQL managed database, and press Enter.

  ![image](https://user-images.githubusercontent.com/73180656/214893649-11c7ea6e-7278-41ba-9bc9-dc196a74ab29.png)

5.	Now, configure WordPress to connect to MySQL database.
6.	Enter the following command to open the wp-config.php file using the Nano text editor:
```
nano /opt/bitnami/wordpress/wp-config.php
```
7.	Scroll down until you find the values for ```DB_USER, DB_PASSWORD, and DB_HOST``` as shown in the following example:

    ![image](https://user-images.githubusercontent.com/73180656/214893910-2d2df62d-4b8b-439b-886b-88500af09adc.png)

8.	Modify the following values:
DB_USER - Edit this to match the user name of your MySQL managed database. 
DB_PASSWORD - Edit this to match the strong password of your MySQL managed database. 
DB_HOST - Edit this to match the endpoint of your MySQL managed database. Be sure to add the :3306 port number at the end of the host address.
9.	Save the file and exit.
10.	 Enter the following command to restart the web services on your instance.
```
sudo /opt/bitnami/ctlscript.sh restart
```
.
    ![image](https://user-images.githubusercontent.com/73180656/214894537-7e1ce14a-1511-46ff-becb-dfa185d4bd30.png)

11.	 After this, WordPress is connected to the MySQL database. Now it will store all its files in RDS.

