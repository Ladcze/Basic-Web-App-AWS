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

---

# Steps (in summary)
- Create Web App
- Build Serverless Function
- Link Serverless Function to Web App
- Create Data Table
- Add Interactivity to Web App

---

# Create the Web App: Deploying static resources for your web application using the AWS Amplify Console.

--The website will be a fairly simple "Hello World" page, with a more functionality added later on. 
--All of your static web content will be hosted by AWS Amplify. The Amplify service is ideal for hosting and deploying static websites. Service users will access the published/hosted site using the URL exposed by Amplify.
--Amplify also provides support for custom domains so this can be implemented (if required). 

• Create an Amplify app
• Upload files for a website directly to Amplify
• Deploy new versions of a webpage with Amplify


Create a new file and Save the file as index.html.
ZIP (compress) only the HTML file
log into the Amplify console. 
5. In the Get Started section, under Host your web app, choose the orange Get started button.
6. Select Deploy without Git provider. This is what you should see on the screen:
7. Choose the Continue button.
8. In the App name field, enter Ladcze's World.
9. For Environment name, enter dev.
10. Select the Drag and drop method. This is what you should see on your screen:
11. Choose the Choose files button.
12. Select the ZIP file you created in Step 3.
13. Choose the Save and deploy button.
14. After a few seconds, you should see the message Deployment successfully completed.


---

 # Building the  Serverless Function (using AWS Lambda).

Using Lambda, a small piece of code will be written in Python, JavaScript, or Java, to be used in a later module to add interactivity to your web page. 
These serverless functions are triggered based on a specific event you will define in the code.

***

What you will accomplish
In this module, you will:
Create a Lambda function from scratch using the AWS console (in Python, JavaScript, or Java)
Create (JSON) events in the AWS console to test your function

***

In a new browser tab, log in to the AWS Lambda console.
It is imperative that the function is created in same regaion as app was deployed. 
Click the Create function button.
Under Function name, enter HelloWorldFunction.
Select Python 3.8 from the runtime dropdown and leave the rest of the defaults unchanged.
6. Choose the orange Create function button.
7. You should see a green message box at the top of your screen with the following message "Successfully created the function HelloWorldFunction."
8. Under Code source, replace the code in lambda_function.py with the following:
9. Save by going to the file menu and selecting Save to save the changes.
10. Choose Deploy to deploy the changes.
11. Let's test our new function. Choose the orange Test button to create a test event by selecting Configure test event.



---
 
 # Linking  Serverless Function to Web App: Deploy your serverless function with API Gateway.

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

# Create Data Table: Persist data in an Amazon DynamoDB table.

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
Following thorugh the above steps, we now have a working web app deployed by Amplify console that can call a Lambda function via API Gateway.   
All the AWS services set up can securely communicate with each other coourtesy the permissions managed/seup within IAM.    
When a user clicks on the Call API button in the web app, it makes a call to our API, which triggers the Lambda function. The Lambda function writes to a database and returns a message to our client via API Gateway. 

![image](https://github.com/Ladcze/Basic-Web-App-AWS/assets/97769275/ea50faf2-ce0a-43f5-b79b-6891e2efd404)

---

# Reference
https://aws.amazon.com/getting-started/hands-on/build-web-app-s3-lambda-api-gateway-dynamodb/
