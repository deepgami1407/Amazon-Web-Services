Steps to host a website in EC2 (Linux) in AWS.
1.	First, we need an EC2 instance to host our website.
2.	Choose Windows Server Base image when creating the instance.

    ![image](https://user-images.githubusercontent.com/73180656/214879657-1ce9aa7d-8ba4-48e9-bbc4-07f45e36b341.png)

3.	Allow http connection during configuration settings and keep everything else as needed.
4.	Connect the instance using RDP client.
5.	Now start IIS (Internet Information Services) from search bar, it is a server manager for windows.

    ![image](https://user-images.githubusercontent.com/73180656/214879601-954c061b-2e21-4152-a630-8a7571a16c9e.png)
    
6.	Now to host a website in this expand to the sites section. 

    ![image](https://user-images.githubusercontent.com/73180656/214879854-367c64ed-9290-4260-95fb-35b52873660d.png)

7.	Now create a sample site named index.html in the C Drive in a folder.
8.	Click on Add Site and give site name, physical path of website.

    ![image](https://user-images.githubusercontent.com/73180656/214879903-fa8f1e73-ee66-4849-91f0-45bc89dff84d.png)

9.	Now the website has been deployed on port 80.
10.	 To access the website on port 80, we need a module called URL Rewrite.
11.	 Download the URL Rewrite module in windows and install it.
12.	 Now we can access the website from the public Ip address of the instance on port 80.

     ![image](https://user-images.githubusercontent.com/73180656/214879986-28861fed-a328-4b56-b27e-096ca129d6f3.png)

13.	 This website is now hosted on port 80 (http), if we want to host it on port 443 (https) we need SSL certificate.
14.	 We can use self signed SSL certificate but it will give a warning on the website, so we need to get issued SSL certificate on the domain name of our website.
15.	 To get a self-signed certificate in go to home page of iis manager and the server certificates and select self-signed certificate.
16.	 Give name of the certificate

     ![image](https://user-images.githubusercontent.com/73180656/214880028-b72c5034-fe60-45cd-9765-99532181a5d5.png)

17.	 Then go to site settings and select bindings and click on add.
18.	 Select https (443) port and select the self-signed certificate and click ok.

     ![image](https://user-images.githubusercontent.com/73180656/214880076-9f24be47-24e8-4839-9425-c0aee994c6a7.png)

19.	 Website hosted using self-signed certificate (Warning because of self-signed certificate)

     ![image](https://user-images.githubusercontent.com/73180656/214880129-ab0b1e7a-0852-464d-bee6-e515c82435e7.png)

