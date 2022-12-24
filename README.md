<h1 ali
    gn="center"> Host a React Application on Amazon S3 and CloudFront</h1>
We’ll be setting up a hosting platform using Amazon S3 and CloudFront, to host a react application.

<h3 align="left">We will do this in 2 simple steps:</h3>

-  **STEP1:** Create the S3 Bucket, Build the Code, and Deploy to S3

-  **STEP2:** Create CloudFront and hook it up with S3

<h3 align="left">How to create an S3 Bucket</h3>
<p align="left">
Let’s login to the AWS Web console. Once logged in, let’s enter s3 into the search field, and click on the s3 service.
1. Here we will click on the Create Bucket button.

2. First we will create a bucket name. The bucket name has to be unique across all AWS customers. Therefore it’s recommended to add some random string to the end of the name.

3. The AWS region, will be the region you want your website to run in. I’m hosting my websites in the US East (N. Virginia) us-east-1. As we are using CloudFront, which will distribute the website globally, the location isn’t that important.

4. We can keep all other options as default and click on the Create bucket button.

You should see now, that the bucket has been created. If we click on it, we see that there are currently no objects in the bucket. In S3 terminology, objects are files and folders.

If you would want to use only HTTP, you could allow public access to your S3 bucket, but we will keep the permissions and other options as default.</p>

<h3 align="left">How to build the code of a React application</h3>
Open the VSCode terminal

We'll be using the create-react-app generato. To use the generator as well as run the React application server, you'll need Node.js JavaScript runtime and npm (Node.js package manager) installed. npm is included with Node.js which you can download and install from Node.js downloads.

**Tip:** To test that you have Node.js and npm correctly installed on your machine, you can type node --version and npm --version in a terminal or command prompt.

**You can now create a new React application by typing:**

npx create-react hello-world 

where hello-world is the name of the folder for your application. This may take a few minutes to create the React application and install its dependencies.

Let's quickly run our React application by navigating to the new folder and typing npm start to start the web server and open the application in a browser:

2. cd my-app
3. npm start

You should see the React logo and a link to "Learn React" on http://localhost:3000 in your browser.

<h3 align="left">How to upload files to the S3 Bucket</h3>
<p align="left">
  We now need to upload this bundle to the S3 bucket. For this go back to the S3 service in the AWS web console, and click on the Upload button.
  
  As you can see the interface is not that user friendly as there are two buttons, one to upload files, and one to upload folders.
  
  It is however possible to just select all the files through the Finder window on Mac, or the Explorer on Windows, and then drag and drop them over. This will include all the files and the folders.
  
  Once done, click on the Upload button to upload the files. 
  
  Now that all the files are uploaded, click on the Close button.
  
  You should now see all your files in the S3 Bucket.
  </p>
  
  <h3 align="left">Create CloudFront CDN Distribution</h3>
  <p align="left">
  Next we will create the CloudFront CDN. Go to the search field, enter cloudfront and click on the service.
  
  You should now see all the CloudFront services. Let’s create a new distribution by clicking on the New Distribution button.
  
  Under Origin Domain search for the S3 bucket name, that you have created. This name is the domain name which points to the S3 HTTP server that runs on your bucket.
  
  Under Origin Access we will choose Origin access control settings.
  
  Click on Create to create the control setting.
  
  Once created you’ll see under Bucket Policy that it says that the policy that needs to be applied to S3 will be provided, after the creation of the distribution.
  
  Under Viewer protocol policy choose Redirect HTTP to HTTPS.
  
  Then click on the Create Distribution button to create the CoudFront distribution.
  
  You should now see a blue box on the top of the page stating that you’ll need to copy the policy to give permissions to CloudFront to access the S3 buckets web server.
  
Click on Copy Policy and head over to the S3 bucket. You can click on the link in the blue box to go to the permissions section of your S3 Bucket.
  
 On the permissions tab of the S3 Bucket scroll down to Bucket Policy and click on the Edit button.
  
Then copy the JSON policy into the Policy field.
  
you click on Save Changes, you’ll see that now the bucket policy has been added.  
  
When your read through the JSON policy it indicates that CloudFront, identified through the AWS Source ARN (which is the CloudFront service identifier), is allowed (through Effect: Allow) to perform the action s3:GetObject (which corresponds to permissions to read the files on the bucket).
  
You’ll now need to wait until the distribution of your website has completed to all the CDN locations. It will take some time, to distribute your website to all the edge servers. Even once the distribution has completed it will usually take another 3-5 minutes, until you can access 
your website with the Distribution Domain Name.
  
In the meantime, let’s go onto the Error pages tab, and make sure, that if there is an error, it’s redirected to a page. In this example I’ll redirect 403 and 404 requests to index.html, but you might want to add error pages to your application and then redirect to those.
  
Let’s add the 403 error and customise the error response.
 
1. Under HTTP Error Code select 403:Forbidden
  
2. Set Customize Error Response to Yes
  
3. Set the Response Page Path to /index.html
  
4. Click the Create custom error response button
  
And let’s do the same with the 404 error response.
  
You should now be able to refresh the Distribution Domain Name in your browser, and the website should appear.
  
<h3>Let’s head back to the S3 Bucket in the AWS Web Console</h3>

Edit static website hosting
1. Under S3 bucket click on Properties
2. Static website hosting will appear at the bottom,click on the edit button
3. Then we will write index.html in the index document
4. Will again write index.html in error document
5. Then click on save changes
  
Then go to CloudFront console and copy a URL of CloudFront distribution domain name,
then paste in web browser now reload the app’s page in the web browser and should see the latest changes.
  
  
  
<h3>Project Link:  https://d1lzabl7vimmj7.cloudfront.net/  </h3>
  
  
  
  
  
  
  
