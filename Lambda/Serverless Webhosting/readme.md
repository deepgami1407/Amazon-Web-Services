**Serverless Website hosting using Lambda and API Gateway**

**Step 1: AWS Lambda setup**
1.	Goto Lambda function and start creating new function.
2.	Enter function name and select runtime engine, here we will select Node.js and create function.
3.	Within the "Function code" box click on the "Actions drop-down menu" and choose: "Upload a .zip file".
4.	Upload the zip file of website (Download from [this link](https://drive.google.com/file/d/1gX7-c8N85nUiQtH6r9iKSjhfsW8SLyQs/view)).

    ![image](https://user-images.githubusercontent.com/73180656/214891986-4e4503c3-5a83-4c26-98f1-c76582b22a40.png)

**Step 2: Amazon API Gateway setup**

1.	Using Amazon API Gateway, we have to map access to a specific resource (URL) with the HTTPS method to the invocation of a Lambda function.
2.	Goto to API Gateway and start building REST API. 
3.	Enter API name and click on create API.
4.	From the left sidebar under your API name choose "Settings" (note: there are 2 "Settings" in the left sidebar, choose the indented one with the smaller font).
5.	At the end of the page, under the "Binary Media Types" heading click on the "+ Add Binary Media Type" and into the input field enter: */*
6.	Save changes.
7.	From the left sidebar under the "API: My Lambda Website" choose "Resources".
8.	From the "Actions drop-down" choose: Create Method.
9.	Choose "ANY" from the drop-down and click on the grey tick icon.
10.	 Make sure the checkbox is checked for the option: "Use Lambda Proxy Integration".
11.	 As "Lambda function" enter the name of your Lambda function: <func_name> and save it.
12.	 From the "Actions drop-down" choose: "Create Resource".
13.	 Make sure the checkbox is checked for the option: "Configure as proxy resource" and create it.
14.	 From the "Actions drop-down" choose: Deploy API.
15.	 As "Deployment stage" choose: [New Stage], as "Stage name" enter: web.
16.	 Click on the blue button "Deploy".
17.	 Copy the "Invoke URL" and run it in the browser.

     ![image](https://user-images.githubusercontent.com/73180656/214892123-16772117-d517-4467-820c-183618f3e895.png)
     
18.  Working Website

     ![image](https://user-images.githubusercontent.com/73180656/214892180-8e78a99b-02fc-45fd-bde0-d2a41697e5dd.png)
