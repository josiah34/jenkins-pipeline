# jenkins-pipeline

In this project I will be setting up a Jenkins pipeline on an AWS ec2 instance. 


1. The first thing that I will do is launch an EC2 ubuntu instance making sure to setup a security group that has inbound rules that allow us to access Jenkins on port 8080. Create an ssh key pair and save the pem file to your machine. 

2. Within user data place this script to setup Jenkins 

```
#!/bin/bash
sudo apt update
sudo apt install openjdk-11-jdk -y
sudo apt install maven -y
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
  
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null

sudo apt-get update
sudo apt-get install jenkins -y


```

3. Next click launch instance and wait for the ec2 instance to fully initialize and run the setup scripts. After a few minutes navigate to ``` http://YOUR-EC2-IP:8080 ```

You will be presented with this screen
![jenkins-setup](https://github.com/josiah34/jenkins-pipeline/assets/25124463/47b837a7-f199-49ed-b53d-4121822fbb51)

4. SSH into your EC2 via your local terminal using your pem key or via the AWS console. Use this command to obtain your Jenkins administrator password. ```sudo cat /var/lib/jenkins/secrets/initialAdminPassword```

5. Finish the setup and install plugins. Create a user admin or continue with the administrator that was created by default. **Make sure oracle jdk plugin is selected along with maven pipeline integration** 
6. Next I will click on manage jenkins then tools as I have to set my JDK path for JDK 8. ```/usr/lib/jvm/java-1.8.0-openjdk-amd64```
7. Set MAVEN version and name within Jenkins. 
8. 


