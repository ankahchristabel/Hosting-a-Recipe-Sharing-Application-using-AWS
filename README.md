# Hosting-a-Recipe-Sharing-Application-using-AWS
deployment process for a recipe-sharing application using AWS CloudFormation templates. 

Hosting the Static Website
A step-by-step look at how I set up my recipe-sharing application using the http deployment:
 	Step 1: Configuring the Frontend
I navigated to the CloudFormation console and selected my template (ch3-http.yaml) for http configuration. I configured the following settings:
•	Create Stack
•	Choose “Upload a template file”.
•	Upload the selected YAML template (ch3-http.yaml)
 

 	Step 2: Configure Stack details
Provide a Stack name ()

 

 	Step 3: Review and Deploy
Review the stack configuration for accuracy.
Acknowledge that CloudFormation may create IAM resources.
Click “Create stack” to initiate the deployment process.
Wait until the stack status changes to “CREATE_COMPLETE”.
 
*** The CloudFormation template provisions the following resources for the applications frontend,backend, and data storage:
Frontend:
Amazon S3,this hosted the static assets(HTML,CSS, ans Javascripts files.
Amazon CloudFront, caching static assets at edge locations globally.
Backend: Public EC2 instance
Data Store:Amazon DynamoDB, which provides a fully managed NoSQL database to store and retrieve saved recipes efficiently.

 	Step 4: Preparing the Application Files
The configuration file contain the variables below:
Variable                                                                   Description
CONFIG_MAX_INGREDIENTS	                    Max ingredients allowed in a recipe
CONFIG_MAX_STEPS	                                Max steps allowed in a recipe
CONFIG_MAX_RECIPES	                                Maximum recipes supported by the application
CONFIG_USER_PAGE_TITLE	                    Title for the user page
CONFIG_ADMIN_PAGE_TITLE	                    Title for the admin page
CONFIG_appConfig	                                            Object with page title and icon
API_URL	                                                      API endpoint used to send requests
In my case I used the public DNS of the EC2 instance which is accessible from the cloudformatiom outputs tab under the APIDNSName output or the EC2 console.
Build the Application
Once the configurations are set, you’ll need to prepare the application files for deployment.

Run the build command for your React application
npm install && npm run build.
 
A /build or /dist folder is created with the compiled application files.
Verify the Build Files
Check and ensure the dist folder contain all necessary files for deployment.


 	Step 6: Uploading to S3
Navigate to the S3 Console
Open the S3 Console
Locate the S3 Bucket
    Find the bucket created by the CloudFormation stack [the bucket name will follow the naming convention defined in the template]
Upload the Files
  Select the contents of the /dist folder’s contents and upload them to the S3 bucket.
 

I selected all the metrics for my CloudFront distribution.
 

Step 6: Testing and Deployment
After setting up everything, I tested my website using the CloudFront URL and it worked flawlessly. However you can use the bucket’s static website URL can equally be used to access the application.
Verify API Connectivity
Test interactions with the backend services to confirm that the API_URL is correctly configured. To test the API_URL, make requests to specific endpoints.
**In my case I used cURL to test the connectivity.
$ curl -i 'https://api.awscloudprojects.site/recipes'

What I Learned Along the Way
1.	Understood how AWS S3, CloudFront, and other services work together to deliver fast, reliable, and scalable websites.
2.	Understand how you can scale automatically, reduce latency, and distribute content globally without managing physical servers is a game-changer for developers.
3.	The few hurdles on this journey taught me more about cloud architecture and the importance of paying attention to detail.
4.	Whether I used http or https configurations, the resulting infrastructure is tailored to meet my application’s specific needs. 
5.	Leveraging the automation and scalability of these AWS Services (CloudFront, S3, and DynamoDB) ensured a reliable and user-friendly platform.


