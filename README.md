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

**In the coming project as we use Docker as a agent , install docker pipeline plugin in Jenkins.**

* Log in to Jenkins.
* Go to Manage Jenkins > Manage Plugins.
* In the Available tab, search for "Docker Pipeline".
* Select the plugin and click the Install button.
* Restart Jenkins after the plugin is installed.

#### Docker Configuration
1. Install Docker
```
sudo apt update
sudo apt install docker.io
```
Docker Deamon by default is accessible to root user. Grant Jenkins user and Ubuntu user permission to docker deamon.

```
sudo su -  # switch to root user
usermod -aG docker jenkins  # creates a group called docker and jenkins is part of docker group
usermod -aG docker ubuntu  # granting ubuntu user permissions to access Docker
systemctl restart docker 
```


### Steps to change Jenkins port from 8080 to 8090 (or any other port)

* First stop the jenkins 
``` 
sudo systemctl restart jenkins
```
1. Locate the Jenkins Configuration File

The port number is usually configured in the Jenkins service file or the Jenkins default configuration file.
For Debian/Ubuntu-based systems:

The configuration file is typically located at:
```
sudo nano /etc/default/jenkins
```
* Find the line: HTTP_PORT=8080 , Change 8080 to 8090
Save and exit the file

Update Firewall Rules (if needed)
If you use a firewall, allow the new port:
```
sudo ufw allow 8090
sudo lsof -i -P -n           // list all the services and their ports
```
Double-check the configuration file to ensure the port was changed correctly.
Verify the HTTP_PORT setting:
```
grep HTTP_PORT /etc/default/jenkins
```
Review Jenkins Systemd Service File. Open the Jenkins service file:
```
sudo nano /lib/systemd/system/jenkins.service
```
Change the jenkins Environment port to = 8090 (whatever port needed)

Then reload daemon and start/restart jenkins
```
sudo systemctl daemon-reload
sudo systemctl restart jenkins
```

