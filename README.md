<h1>Deployment 3 Done by: Nehemiah Monrose | 16th.09/2023</h1>
<h2>How to set up a Jenkins server and deploy an application to AWS Elastic Beanstalk</h2>


[link to deployment files](/main)

<h2>Purpose</h2>
<p>The purpose of this deployment is to set up Jenkins Server and Deploy an Application on AWS Elastic Beanstalk. 
This time I also added a deploy stage in my Jenkinsfile and added a webhook which is used to add two applications together.
</p>
<h2>Issues</h2>
<p>While doing the deployment I came across an issue where I was trying to run sudo  while logged in as a jenkins user.
It kept on saying that "jenkins is not a sudoer" meaning that this user does not have sudo rights. so to fix this issue I switched
back to the ubuntu user and ran this code : echo 'jenkins ALL=(ALL) ALL' >> /etc/sudoers | Then switched back to jenkins user and ran my codes successfully. </p>

<h2>Steps</h2>
<em>Before we start our steps we must create a new repository and store our deployment files,create our EC2 instance for deployment3 and then we begin our deployment steps:</em>




### Step 1: Create a Jenkins server

1. Install Jenkins on our server.
2. Install the following dependencies:
* `python3.10-venv`
* `python-pip`
* `unzip`

### Step 2: Create a multibranch pipeline

1. In Jenkins, go to **New Item** and select **Multibranch Pipeline**.
2. Enter a name for your pipeline.
3. Under **Branch Sources**, select **GitHub**.
4. Enter your GitHub repository URL and credentials.
5. Click **Save**.

### Step 3: Run the build

1. Click the **Build Now** button.
2. The build will start running.
3. Once the build is complete, you will see a status message.

### Step 4: Install the AWS EB CLI

1. SSH into your Jenkins server.
2. Install AWS Elastic Beanstalk CLI.Follow the steps in the official installation guide: AWS Elastic Beanstalk CLI Installation.
3. Configure your AWS Elastic Beanstalk credentials using eb init and eb create commands as needed.


### Step 5: Add the Deploy stage to your Jenkinsfile

1. Add the following stage to your Jenkinsfile:


​
stage ('Deploy') {
  steps {
    sh '/var/lib/jenkins/.local/bin/eb deploy'
  }
}
​


### Step 6: Rerun the build

1. Click the **Build Now** button.
2. The build will start running.
3. Once the build is complete, you will see a status message.

### Step 7: Verify the deployment

1. If your application redeployed successfully, you will see a message saying:


​
Application deployed successfully.
​

### Step 8: Configure a webhook

1. Navigate to main repo settings
2. Click Payload Url
3. Paste this code: http:// 3.92.240.88:8080/github-webhook/
4. Add webhook and youre done!

<h2>The change I noticed when I redeployed</h2>

<p>I noticed that there were 2 applications on one webpage now.
There was only the url shortener application in the beginning of the deployment and after redeploying I noticed that was a 
second application called **File**.</p>


<img width="1439" alt="Screenshot 2023-09-15 at 11 46 51 PM" src="https://github.com/NMonKLabs77/deployment3/assets/139259756/29463a69-549a-4c64-9d59-66b19947adda">

<h2>Systems Diagram</h2>

![Deploy3-nene drawio](https://github.com/NMonKLabs77/deployment3/assets/139259756/752c6c7f-e5b8-4ae2-896a-592e070f03c2)

<h2>Optimisation</h2>
<p>I would fully automate this process instead of painstakingly manually doing all the steps of Devops manually. 
I would also use a dashboard and platform to keep all my process sort of like a admin project management platform so that I would have all 
my projects in one place.</p>




