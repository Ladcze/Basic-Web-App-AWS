# Basic-Web-App-AWS
A static web app that rendering "Ladcze's World" with some in-built API functionalities

--- 

# Introduction
This project is a simple web application comprising a static web app that renders "Ladcze's World".
The output returned will be based on custom input as provided using some functionalities built into the app. 
Below is a snapshot of what the final project looks like   

![image](https://github.com/Ladcze/Basic-Web-App-AWS/assets/97769275/3524d107-5309-425e-af0f-b92377480672)

---

# Application Architecture
The diagram below provides a visual representation of the services used in this tutorial and how they are connected. 
![image](https://github.com/Ladcze/Basic-Web-App-AWS/assets/97769275/aca262b1-12c1-4979-94d0-870fec16ce67)

---

# Services deployed
The key services required (including an AWS account with administrator level access) for this project are the 
- AWS Amplify 
- AWS IAM
- Amazon API Gateway
- AWS Lambda
- Amazon DynamoDB

![aws_amplify](https://github.com/Ladcze/Basic-Web-App-AWS/assets/97769275/fbd48586-5230-402d-83f8-a8425b744aec)  ![aws_iam](https://github.com/Ladcze/Basic-Web-App-AWS/assets/97769275/b9d69897-fdc5-4330-ab0e-4bd8af2547f5)  ![amazon_api_gateway](https://github.com/Ladcze/Basic-Web-App-AWS/assets/97769275/65959073-c8b9-4254-aaa4-eb57e218e728)  ![aws_lambda](https://github.com/Ladcze/Basic-Web-App-AWS/assets/97769275/386ecaf1-edeb-42b7-89de-d001f2eeb6ff)  ![amazon_dynamodb](https://github.com/Ladcze/Basic-Web-App-AWS/assets/97769275/d0837914-2516-4769-9c9c-c612f7fc25c2)

---

# Steps (in summary)
- Create Web App
- Build Serverless Function
- Link Serverless Function to Web App
- Create Data Table
- Add Interactivity to Web App   

For the purpose of this project, it's imperative all services are deployed within the same region/location. 

---

# 1. Create the Web App: Deploying static resources for your web application using the AWS Amplify Console.
AWS Amplify is an AWS offering/service used to develop and deploy cloud-powered mobile and web apps. It provides a continuous delivery and hosting service for web applications.   

Create a new file and save the file as index.html; and have it zipped in ready for upload to Amplify.    
The website is a fairly simple "Hello World" page, with more functionality added later on. The said basic static webpage will be hosted by AWS Amplify. The Amplify service is ideal for hosting and deploying static websites. Service users will access the published/hosted site using the URL exposed by Amplify. Amplify also provides support for custom domains so this can be implemented (if required). This will implemeneted later on.   

-  - Create an Amplify app.

Log into the Amplify console.   
In the Get Started section, under Host your web app, choose the orange Get started button.   
Select Deploy without Git provider    
![image](https://github.com/Ladcze/Basic-Web-App-AWS/assets/97769275/a799eaaa-8c89-49f8-9541-689516333e59) 
   
Enter a name for the app (Ladcze's World) and set environment name (Test or Dev).   
Upload the zipped file for the website directly onto Amplify.   
Choose the Save and deploy button.   
![image](https://github.com/Ladcze/Basic-Web-App-AWS/assets/97769275/877ae2a8-f3fd-473a-8ae3-1e1adee5bbdf)

After a few seconds, you should see the message Deployment successfully completed.
![image](https://github.com/Ladcze/Basic-Web-App-AWS/assets/97769275/2e9303ea-8424-48fe-bfe8-7c3f66156d98)


 <!-- -  - Deploy new versions of a webpage with Amplify -->

---

# 2. Building the Serverless Function (using AWS Lambda).
AWS Lambda is an event-driven, serverless computing service that runs code in response to events and automatically manages the computing resources required by that code.   

With Lambda, a small piece of code is written in Python. This will be used at a later time to add interactivity to the webpage/app created. These serverless functions are triggered based on a specific event to be defined within the code.   

-  - Create a Lambda function from scratch using the AWS console (in Python)   

Log into the AWS Lambda console.   
Click the Create function button.   
Under Function name, enter LadczeWorldFunction.   
Select Python 3.11 from the runtime dropdown and leave the rest of the defaults unchanged.   

![image](https://github.com/Ladcze/Basic-Web-App-AWS/assets/97769275/d1fc99ca-8238-40c0-9260-6a9197b66dae)

Choose the orange Create function button.   
You should see a green message box at the top of your screen with the following message "Successfully created the function LadczeWorldFunction."   

![image](https://github.com/Ladcze/Basic-Web-App-AWS/assets/97769275/15b6c5d9-78aa-4c6c-843f-10ebad0bbbf7)   

   

-  - Create (JSON) events in the AWS console to test your function.   

Under Code source, replace the code in lambda_function.py with the following: (see LambdaFunction.py in repo).   
Save (using File-save menu) to implement the changes.   

![image](https://github.com/Ladcze/Basic-Web-App-AWS/assets/97769275/393ab3c4-f9e0-4cd6-8bb6-618ad2f390fd)    

Choose Deploy to deploy the changes.   
![image](https://github.com/Ladcze/Basic-Web-App-AWS/assets/97769275/173aeae8-ecc7-4a83-9431-2852f3bf3d89)


A quick test of the new function (using the orange Test button) to create a test event (after configuring a test event) is successful.   
![image](https://github.com/Ladcze/Basic-Web-App-AWS/assets/97769275/5ff2f207-c17d-4881-857e-450cdc9f904f)


---
 
 # 3. Linking Serverless Function to Web App: Deploying the serverless function with API Gateway.

 use Amazon API Gateway to create a RESTful API that will allow us to make calls to our Lambda function from a web client 
The API Gateway acts as a middle layer between the front-end (web app) and the serverless back-end (function).   


--Create a new API using API Gateway
--Define HTTP methods on your API
--Trigger a Lambda function from an API
--Enable cross-origin resource sharing (CORS) on an API so you can consume resources from a different origin (domain)
--Test an API created with API Gateway from the AWS Management Console

******

Log in to the API Gateway console.
In the Choose an API type section, find the REST API card and choose the Build button on the card.
Under Choose the protocol, select REST.
Under Create new API, select New API.
In the API name field, enter HelloWorldAPI.
Select Edge optimized from the Endpoint Type dropdown. (Note: Edge-optimized endpoints are best for geographically distributed clients. This makes them a good choice for public services being accessed from the internet. Regional endpoints are typically used for APIs that are accessed primarily from within the same AWS Region.)
Choose the blue Create API button. Your settings should look like the accompanying screenshot.


In the left navigation pane, select Resources under API: HelloWorldAPI.
Ensure the "/" resource is selected.
From the Actions dropdown menu, select Create Method.
Select POST from the new dropdown that appears, then select the checkmark.
Select Lambda Function for the Integration type.
Select the Lambda Region you used when making the function (or else you will see a warning box reading "You do not have any Lambda Functions in...").
Enter HelloWorldFunction in the Lambda Function field.
Choose the blue Save button.
You should see a message letting you know you are giving the API you are creating permission to call your Lambda function. Choose the OK button.
With the newly created POST method selected, select Enable CORS from the Action dropdown menu.
Leave the POST checkbox selected and choose the blue Enable CORS and replace existing CORS headers button.
You should see a message asking you to confirm method changes. Choose the blue Yes, replace existing values button.


In the Actions dropdown list, select Deploy API.
Select [New Stage] in the Deployment stage dropdown list.
Enter dev for the Stage Name.
Choose Deploy.
Copy and save the URL next to Invoke URL (you will need it in module five).


In the left navigation pane, select Resources.
The methods for our API will now be listed on the right. Choose POST.
Choose the small blue lightning bolt.
Paste the following into the Request Body field:
5. Choose the blue Test button.
6. On the right side, you should see a response with Code 200.
7. Great! We have built and tested an API that calls our Lambda function.

Summary/Note - We added API Gateway and connected it to our existing Lambda function. Now, we can trigger our function with an API call. We are still missing the ability to generate this call from our web client.

---

# 4. Create Data Table: Persist data in an Amazon DynamoDB table.

we will create a table to persist data using Amazon DynamoDB. DynamoDB is a key-value database service, so we do not need to create a schema for our data. It has consistent performance at any scale and there are no servers to manage when using it.   

Additionally, we will use the AWS Identity and Access Management (IAM) service to securely give our services the required permissions to interact with each other. Specifically, we are going to allow the Lambda function we created in module two to write to our newly created DynamoDB table using an IAM policy. To do this, we will use the AWS SDK (Python, JavaScript, or Java) from our Lambda function   

Create a DynamoDB table using the AWS Management Console
Create a role and manage permissions with IAM
Write to a DynamoDB table using the AWS SDK (Python, JavaScript, or Java)   


Log in to the Amazon DynamoDB console.
Make sure you create your table in the same Region in which you created the web app in the previous module. You can see this at the very top of the page, next to your account name.
Choose the orange Create table button.
Under Table name, enter HelloWorldDatabase.
In the Partition key field, enter ID. The partition key is part of the table's primary key.
Leave the rest of the default values unchanged and choose the orange Create table button.
In the list of tables, select the table name, HelloWorldDatabase.
In the General information section, show Additional info by selecting the down arrow.
9. Copy the Amazon Resource Name (ARN). You will need it later in this module.   

***

Now that we have a table, let's edit our Lambda function to be able to write data to it. In a new browser window, open the AWS Lambda console.
Select the function we created in module two (if you have been using our examples, it will be called HelloWorldFunction). If you don't see it, check the Region dropdown in the upper right next to your name to ensure you're in the same Region you created the function in.
We'll be adding permissions to our function so it can use the DynamoDB service, and we will be using AWS Identity and Access Management (IAM) to do so.
Select the Configuration tab and select Permissions from the right side menu.
In the Execution role box, under Role name, choose the link. A new browser tab will open.
In the Permissions policies box, open the Add permissions dropdown and select Create inline policy.
Select the JSON tab.
Paste the following policy in the text area, taking care to replace your table's ARN in the Resource field in line 15:
9. This policy will allow our Lambda function to read, edit, or delete items, but restrict it to only be able to do so in the table we created.
10. Choose the blue Review Policy button.
11. Next to Name, enter HelloWorldDynamoPolicy.
12. Choose the blue Create Policy button.
13. You can now close this browser tab and go back to the tab for your Lambda function.   


***

test the changes

Choose the orange Test button.
You should see an Execution result: succeeded message with a green background.
In a new browser tab, open the DynamoDB console.
In the left-hand navigation pane, select Tables > Explore items.
Select HelloWorldDatabase, which we created earlier in this module.
Select the Items tab on the right.
Items matching your test event appear under Items returned. If you have been using our examples, the item ID will be Hello from Lambda, Ada Lovelace or Ada Lovelace.
Every time your Lambda function executes, your DynamoDB table will be updated. If the same name is used, only the time stamp will change.

***

Summary/Note - We added two services in this module: DynamoDB (for storage) and IAM (for managing permissions securely). Both are connected to our Lambda function, so that it can write to our database. The final step is to add code to our client to call the API Gateway.


---

 # Add Interactivity to Web App: Modifying your web app to invoke your API.

 will update the static website we created in module one to invoke the REST API we created in module three. This will add the ability to display text based on what you input.   

Call an API Gateway API from an HTML page
Upload a new version of a web app to the Amplify console   

***

Open the index.html file you created in module one.
Replace the existing code with the following: ""see code base""
3. Make sure you add your API Invoke URL on Line 41 (from module three). Note: If you do not have your API's URL, you can get it from the API Gateway console by selecting your API and choosing stages.
4. Save the file.
5. ZIP (compress) only the HTML file.
6. Open the Amplify console.
7. Choose the web app created in module one.
8. Choose the white Choose files button.
9. Select the ZIP file you created in Step 5.
10. When the file is uploaded, a deployment process will automatically begin. Once you see a green bar, your deployment will be complete.   

***
Test updated web app
Choose the URL under Domain.
Your updated web app should load in your browser.
Fill in your name (or whatever you prefer) and choose the Call API button.
You should see a message that starts with Hello from Lambda followed by the text you filled in.   
 

--- 

# Conclusion/Summary
Following through the above steps, we now have a working web app deployed by Amplify console that can call a Lambda function via API Gateway.   
All the AWS services set up can securely communicate with each other coourtesy the permissions managed/seup within IAM.    
When a user clicks on the Call API button in the web app, it makes a call to our API, which triggers the Lambda function. The Lambda function writes to a database and returns a message to our client via API Gateway. 

![image](https://github.com/Ladcze/Basic-Web-App-AWS/assets/97769275/ea50faf2-ce0a-43f5-b79b-6891e2efd404)

---

# Reference
https://aws.amazon.com/getting-started/hands-on/build-web-app-s3-lambda-api-gateway-dynamodb/
