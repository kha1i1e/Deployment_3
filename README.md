# **Automating Jenkins Build and AWS Beanstalk Deployment with Webhooks:**

# Purpose:

> ### The goal of this project is to automate the build and deployment stages within a CI/CD pipeline. This automation eliminates manual tasks and minimizes the chances of human errors. To achieve this, we configure a mechanism to regularly check the code repository at specified intervals. Additionally, I utilized Webhooks to inform Jenkins whenever new code is pushed to my GitHub repository. Both of these methods work together seamlessly to automatically build, test, and redeploy my application, significantly reducing deployment time and labor costs.
> ### The app's primary objective is to convert lengthy URLs into concise and user-friendly links, thereby promoting easier sharing and enhanced usability. To achieve this, we employ Jenkins to enforce error-free deployments, while AWS Beanstalk efficiently manages and auto-scales our infrastructure, ensuring uninterrupted availability. These tools allowed me to address user engagement-related business challenges and streamline my workflow.

### URL Shortener:
> Frequently, URLs can become unwieldy and unfriendly to users. A URL shortening service resolves this issue by transforming lengthy URLs into more compact and manageable forms. Consequently, this enhances user engagement, as shorter URLs are not only more user-friendly but also more likely to be shared. Nevertheless, it's important to note that shortened URLs have historically been associated with security risks from viruses and malicious websites. However, users are increasingly accustomed to encountering shortened URLs, which ultimately leads to greater engagement with my content.

### Jenkins:
> Manual processes for building, testing, and deploying applications are susceptible to human error and often consume significant amounts of time. Jenkins, my automation tool of choice, automates these critical phases, mitigating the risk of human error and expediting our continuous integration and deployment capabilities. While there may be a learning curve associated with Jenkins, the investment in learning this tool ultimately reduces the overall cost and time required to build and deploy the application.

### Webhook: 
> Webhooks are a crucial component in the context of continuous integration and continuous deployment (CI/CD). Webhooks automate the triggering of actions in response to events. In your case, you want Jenkins to automatically start the deployment process whenever there's a new commit or code change in your GitHub repository. Without a webhook, you'd have to manually initiate the Jenkins build each time, which is not efficient, especially in a CI/CD workflow. Webhooks provide real-time updates. As soon as a relevant event occurs (e.g., a new commit is pushed to the repository), the webhook sends a payload to the configured URL (in this case, my Jenkins server), allowing for immediate action. This ensures that your deployments are as up-to-date as possible. 

### AWS Beanstalk:
> The management of infrastructure for continuous application deployment can be both time-consuming and intricate, with escalating costs as complexity increases. AWS Beanstalk takes on the responsibility of overseeing our application's infrastructure, allowing your team concentrate on coding and implementing new features. This seamless infrastructure management ensures that the application can scale efficiently and remain consistently available to the users.


## Plan Diagram
![Deployment 3 Diagram drawio](https://github.com/atlas-lion91/Deployment_3/assets/140761974/0cb466f1-c771-4bde-b1bf-ce98caadab32)

___

# Steps:
## 1. Clone Source Code & Set Up a New GitHub Repository
> ````
> git --version
> git clone https://github.com/kura-labs-org/c4_deployment-3.git
> sudo apt install gh
> gh auth login
> gh repo create Deployment_3 --public
> mkdir Deployment_3
> cp -r c4_deployment-3/* Deployment_3/
> cd Deployment_3/
> git init
> git add .
> git commit -m "Initial commit"
> git branch -M main
> git remote add origin https://github.com/atlas-lion91/Deployment_3
> git push -u origin main
> cd ~
> ````

## 2. Install Jenkins
> ````
> sudo apt install openjdk-11-jdk
> apt-get update
> sudo apt-get update
> curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee     /usr/share/keyrings/jenkins-keyring.asc > /dev/null
> echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]     https://pkg.jenkins.io/debian binary/ | sudo tee     /etc/apt/sources.list.d/jenkins.list > /dev/null
> sudo apt-get update
> sudo apt-get install fontconfig openjdk-17-jre
> sudo apt-get install jenkins
> sudo systemctl start jenkins
> sudo cat /var/lib/jenkins/secrets/initialAdminPassword
> ````

## 3. Install Python, Pip, and Unzip
> ````
> sudo apt update
> sudo apt install python-pip
> sudo apt install python3.10-venv
> sudo apt install unzip
> pip3 --version
> python3.10 -m venv --version
> ````

## 4. Configure Multi-Branch Jenkins Pipeline
> ````
> # Log into the Jenkins server
> # Access the dashboard
> # Click "New Item"
> # Provide a project name
> # Select "Multibranch Pipeline," then click "Ok"
> # Click "Add Source" and choose "GitHub"
> # Click "Add" next to 'Credentials'
> # Enter your GitHub repository details, username, and use a GitHub token as the password
> ````

## 5. Install AWS CLI
> ````
> curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
> unzip awscliv2.zip
> sudo ./aws/install
> aws --version
> aws configure



## 6. Configure Jenkins User
> ````
> sudo passwd jenkins
> sudo su - jenkins -s /bin/bash
> ````

## 7. Install AWS Beanstalk CLI
> ```
> pip install awsebcli --upgrade --user
> export PATH=$PATH:$HOME/.local/bin
> eb --version
> aws configure
> ```

## 8. Initialize and Create AWS Beanstalk Environment
> ```
> cd workspace/
> ls
> cd Deployment_3

_main
> ls
> eb init
> eb create
> ```

## 9. Add Deployment Stage to Jenkins File
> ````
> sudo apt update
> sudo apt install python-pip
> sudo apt install python3.10-venv
> sudo apt install unzip
> pip3 --version
> python3.10 -m venv --version
> ````

## 10. Configure Webhook
> ````
> # Log into GitHub
> # Open the project repository
> # Navigate to Settings > Webhooks > Add Webhook
> # Enter the payload URL
> # Select "application/json"
> # Choose "just the push event"
> # Click "Add Webhook"
> # Verify the 200 response from the Webhook ping
> ````

## 11. Push New Code to Automate changes in Jenkins Build
> ````
> # Change directories into the templates folder
> cd Deployment_3/templates/       
> # Open the base HTML file to make an edit to the body of the home page of our app
> nano base.html          
> # I changed the background color of the home page to red, then pushed to GitHub
> 
> git add .
> git commit -m 'Commit a change'
> git push origin HEAD:
> ````

### URL Shortener Initially Deployed Webpage
![URL Shortener Web App confirmation](https://github.com/atlas-lion91/Deployment_3/assets/140761974/0e2e2dfb-eb43-4fa7-9778-22f7564a9bf3) 

### URL Shortener Webpage after edits Deployed with Webhook
  ![Screenshot 2023-09-16 080113](https://github.com/atlas-lion91/Deployment_3/assets/140761974/39b0184e-d6bd-40ce-bf75-29f50f7ef605) 

## On the Jenkins server, we can see that a build, test, and deployment were automatically triggered.

> <p align="center">
![Screenshot 2023-09-16 002247](https://github.com/atlas-lion91/Deployment_3/assets/140761974/5904e395-9dcd-4801-9aa6-02e78a5ac8f0)
> </p>

---

# Issues:

### _1) Webhook Payload URL Response:_
> ##### I configured a webhook in GitHub to notify Jenkins, triggering the build, test, and deployment process whenever code changes were pushed to GitHub. In the image below, you can see that we needed to specify a URL:

### Initially, I entered the URL of the application as the payload URL, which resulted in a 403 error response.

### I learned that the payload URL should be the URL of our Jenkins server, formatted as follows:

> #### (http://yourip:8080/github-webhook/)  

![Screenshot 2023-09-16 001807](https://github.com/atlas-lion91/Deployment_3/assets/140761974/f2547007-e52a-420d-a3e5-562194313309)


---

# Optimization:

<aside>
To optimize this project further, I would add scripting for repetitive tasks. Creating scripts or shell commands for repetitive tasks, such as environment setup, software installation, and repository cloning will make it easier to automate these steps and reduce the risk of human error.
</aside>
