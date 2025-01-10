# Welcome to the Jenkins-CI-CD 

### Step-1
#### Create AWS EC2 Instance 
* Go to AWS Console
* Launch instance
* Allow port 22 for SSH , 8080 for Jenkins in EC2 Security Groups
* SSH into the instance using Mobaxterm

### Step-2 : Install Jenkins
* Pre-Requisites: Java (JDK)

Run the below commands to install Java and Jenkins

**Install Java**

```
sudo apt update
sudo apt install openjdk-17-jre
```
Verify Java is Installed
```
java -version
```
**Now Install Jenkins**
```
curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins
```
* Login to Jenkins using this URL - **http://<EC2Instance_publicIP>:8080/**
* Jenkins runs on port 8080
* After login to Jenkins, - Run the command in terminal (Mobaxterm) to copy the Jenkins Admin Password - 
* ```sudo cat /var/lib/jenkins/secrets/initialAdminPassword```
* Enter the Administrator password to Jenkins
* Install suggested plugins
* Create First Admin User
