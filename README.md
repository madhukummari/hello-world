# 1 Module Setting Tomcat and Jenkins Up and Running

##################################################################################
## Jenkins Setup
#!/bin/bash
# Setup Hostname
sudo hostnamectl set-hostname "jenkins.cloudbinary.io"
# Update the hostname part of Host File
echo "`hostname -I | awk '{ print $1 }'` `hostname`" >> /etc/hosts
# Update Ubuntu Repository
apt update
# Download, & Install Utility Softwares
apt install git wget unzip curl tree -y
# Download, Install Java 11
sudo apt install openjdk-11-jdk -y
# Backup the Environment File
sudo cp -pvr /etc/environment "/etc/environment_$(date +%F_%R)"
# Create Environment Variables
echo "JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64/" >> /etc/environment
# Compile the Configuration
source /etc/environment
# Download, Install Maven
sudo apt-get install maven -y
# Backup the Environment File
sudo cp -pvr /etc/environment "/etc/environment_$(date +%F_%R)"
# Create Environment Variables
echo "MAVEN_HOME=/usr/share/maven" >> /etc/environment
# Compile the Configuration
source /etc/environment
# Go to /opt directory to download Jenkins
# cd /opt/
# Add Jenkins Repository
sudo wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
# Adding the Jenkins Remote Repository URL in Ubuntu Local Repository Configuration file
sudo sh -c 'echo deb https://pkg.jenkins.io/debian-stable binary/' > /etc/apt/sources.list.d/jenkins.list
# Update the Repository on Ubuntu 18.04
sudo apt update
# Download, Install Jenkins
sudo apt install jenkins -y
# Verify the jenkins service
# sudo systemctl status jenkins.service
# Enable Jenkins Daemon/Service at Boot
# sudo systemctl enable jenkins.service
# Restart the Jenkins Daemon/Service
# sudo systemctl restart jenkins.service
# Usig Process Status Command
# ps -aux | grep jenkins

#############################################################################################################
# 2 Module Integrating Jenkins With Git

go to manage jenkins
install git hub plugin if not exists

after re starting jenkins 
go to manage jenkins > Global tool configuration > git

apply and save

in source code management of denkins new project add git hub repo link
https://github.com/kesavkummari/javawebapplication.git


# 3 setting ups Maven for jenkins Server

install maven plugin 
and set path of maven and java in global tool configuration

# 3 setting ups Maven for tomcat Server


#!/bin/bash
# Setup Hostname 
sudo hostnamectl set-hostname "dev.cloudbinary.io"

# Update the hostname part of Host File
echo "`hostname -I | awk '{ print $1 }'` `hostname`" >> /etc/hosts 

# Update Ubuntu Repository 
apt update 
# Download, & Install Utility Softwares 
apt install git wget unzip curl tree -y 
# Download, Install Java 11
sudo apt-get install openjdk-11-jdk -y
# Backup the Environment File
sudo cp -pvr /etc/environment "/etc/environment_$(date +%F_%R)"
# Create Environment Variables 
echo "JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64/" >> /etc/environment
# Compile the Configuration 
source /etc/environment
# Go to /opt directory to download Apache Tomcat 
cd /opt/
# Download Apache Tomcat - Application
sudo wget https://downloads.apache.org/tomcat/tomcat-8/v8.5.84/bin/apache-tomcat-8.5.84.tar.gz
# Extract the Tomcat File
sudo tar xvzf apache-tomcat-8.5.84.tar.gz
# Rename the Tomcat Folder
sudo mv apache-tomcat-8.5.84 tomcat
# Go Inside the Tomcat Folder
cd /opt/tomcat/
# Take Tomcat Configuration as backup 
sudo cp -pvr /opt/tomcat/conf/tomcat-users.xml "/opt/tomcat/conf/tomcat-users.xml_$(date +%F_%R)"
# To delete last line and which contains </tomcat-users>
sed -i '$d' /opt/tomcat/conf/tomcat-users.xml
#Add User & Attach Roles to Tomcat 
echo '<role rolename="manager-gui"/>'  >> /opt/tomcat/conf/tomcat-users.xml
echo '<role rolename="manager-script"/>' >> /opt/tomcat/conf/tomcat-users.xml
echo '<role rolename="manager-jmx"/>'    >> /opt/tomcat/conf/tomcat-users.xml
echo '<role rolename="manager-status"/>' >> /opt/tomcat/conf/tomcat-users.xml
echo '<role rolename="admin-gui"/>'     >> /opt/tomcat/conf/tomcat-users.xml
echo '<role rolename="admin-script"/>' >> /opt/tomcat/conf/tomcat-users.xml
echo '<user username="admin" password="redhat@123" roles="manager-gui,manager-script,manager-jmx,manager-status,admin-gui,admin-script"/>' >> /opt/tomcat/conf/tomcat-users.xml
echo "</tomcat-users>" >> /opt/tomcat/conf/tomcat-users.xml
# Start Tomcat Server
cd /opt/tomcat/bin/

./startup.sh



edit context.xml files to access manager and host manager apps under tomcat webapp directory

edit users.xml files from tomcat conf directory

# 2 Module Integrating Jenkins With TomCat

install Plugin Deploy to container 
configuring tomcat using credenmanage (credentialstials)

create with tomcat 8x

# 2 Module automating the 

install Plugin Deploy to container 
configuring tomcat using credenmanage (credentials)

create with tomcat 8x