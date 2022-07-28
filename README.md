# CORS-Fix-Firebase-Cloud-Storage-Access-
This json will fix the CORS issue that arises when it accessed in Cross-Origin 

# What Is Firebase Storage?
Firebase storage is file storage area where user can generate and store their files, also it helps the users to keep their information safe yet available in the cloud. Basically, it’s free version gives you 100 MB memory for data storage and a maximum of 50 connections. Where as Amazon S3 bucket also gives us cloud file storage but it doesn’t give us free storage.

#Why do we need to use Firebase storage?
Firebase also has a CDN(Content delivery networks) and the CND is system of distributed servers network and it delivers the pages and other web content to the user based on their geographic locations. Using this firebase storage works faster when comparing to Amazon S3 bucket.

# CORS Issue
Sometimes the files we upload on the firebase storage can’t be accessed, it can be simply viewed but we will not have access to modify or access when it is necessary. CORS (Cross-Origin Resource Sharing) is one of the best solution to overcome this issue which helps to access web resources from different domains.

# How to fix firebase storage CORS issue?
To fix CORS issue you have to do following steps, final result will be problem solved,

# Step 1: Install gsutil tool
gsutil:
gsutil is a Python application, a tool which will enable us to access the Cloud Storage from command-line.
Installing gsutil as part of the Google Cloud SDK:

# LINUX:
#1. Enter the following at a command prompt:

$ curl https://sdk.cloud.google.com | bash
#2. Restart your shell:

$exec -l $SHELL
 
#3. Run gcloud init to initialize the gcloud environment:

$gcloud init
 
Use components update command to update gcloud components:

$gcloud components update
 

# Step 2: We must authenticate (OAuth 2.0) Google Cloud SDK to access firebase project
Incase if you already ran `gcloud init` , then you will be asked whether you want to re-initialize the configuration or like to create a new one.
1. Open a command prompt instance.
2. Run `gcloud init` in command prompt.
Once you run, you will receive the following message:

   Welcome! This command will take you through the configuration of gcloud.
 
   Your current configuration has been set to: [default]
 
   To continue, you must login. Would you like to login (Y/n)?
 
3. You can type “Y” to log in.
As soon as you enter “Y”, the command will print a URL which will try to open a browser window. Again, this will request to access your project so you can give access and open. For example, this will show you a message like this,

Your browser has been opened to visit:
 
   https://accounts.google.com/o/oauth2/auth?redirect_uri=http%3A%2F%2F
 
 

Let’s see how to give access
By chance, if you’re working on a local machine then your browser will not defaultly load the URL so we must retry it using “gcloud init command with the –console-only flag” as follows,

  gcloud init --console-only
 
Sometimes the Cloud SDK will detect and say that, this browser can’t be opened with the following link,
https://accounts.google.com/o/oauth2/auth?redirect_uri=urn%3Aietf%3Awg%3A

Go to the following link in your browser & enter a verification code. After all, open the browser and navigate to the URL provided.
4. If it prompted then you can directly sign in with the Google account associated with your Cloud Storage data and grant access.
If the browser window opened automatically, review the application permissions and click accept when you are ready. The verification code is then automatically sent to the command line tool.
Otherside, if you’re working on a remote machine or used “console-only flag”, then you just copy the verification code from the URL and paste it in terminal command line. Finally, there you can enter the verification code.
2.6 Choose the default project for this configuration.
Once you done with all this configuration, you will be prompted to choose list of available project so there you can choose the project & project Id from the list.
After fixing this property, gsutil will require a project, such as gsutil mb, so you can use the default project ID and in case you like to override them with the -p flag then you can choose appropriate ID or set the CLOUDSDK_CORE_PROJECT environment variable.
Ref: https://cloud.google.com/storage/docs/gsutil_install

# Step 3: Configure Cross-Origin Resource Sharing (CORS)
We can use the gsutil cors command to configure CORS on a bucket:
gsutil cors set cors.json gs://mlc-agira-271a8.appspot.com

cors.json will contain:
  [
   {
     "origin": ["*"],
     "method": ["GET"],
     "maxAgeSeconds": 3600
   }
 ]
 
Note: For the json field `origin`, we can setup the necessary domain name based on our interest but here we have allowed all the domains(`*`).
Ref: https://cloud.google.com/storage/docs/configuring-cors
Hopefully, now you can able to access the files in firebase storage and i believe this might you understand and fix the issue much better
