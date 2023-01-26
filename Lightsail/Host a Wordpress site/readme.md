**WordPress in LightSail**

1.	Go to LightSail and create instance.
2.	Select Platform as Linux/Unix.
3.	Select blueprint as WordPress.
4.	Create SSH key pair for the instance.
5.	Choose instance plan and assign name to the instance.
6.	Click on create instance and WordPress is installed and ready to use.
7.	Connect the using ssh and get the password for the WordPress website.
8.	After connecting to the instance enter the following command to see the password of the WordPress website:
```
cat bitnami_application_password
```
.
     ![image](https://user-images.githubusercontent.com/73180656/214892864-1788d282-17c4-4e4a-847a-040b87b027a8.png)

9.	In a browser window, go to:
```
http://PublicIpAddress_of Instance/wp-login.php
```
10.	 In the Username or Email Address box, enter ```user```.
11.	 In the Password box, enter the default password obtained earlier in this tutorial.
12.	 Choose Log in.

     ![image](https://user-images.githubusercontent.com/73180656/214893096-3f7ace99-9a8d-479e-9209-03d11467f556.png)
