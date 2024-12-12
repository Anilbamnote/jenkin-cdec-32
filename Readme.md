# Jenkins
SDLC - Software Development Life Cycle Req Gather and Analysis Plan and Design Coding and Implimentation Test Deliver and Deploy Monitoring and Maintainers

Coding:

java application:

main.java -> syntax check -> integrate -> compile -> .jar -> run .java .java

syntax -> integrate -> compile -> .jar -> Deploy Server

main.java -> .jar (ERP)

dev (server) -> deplpoy

Automate - CI-CD
Continuous Integration

java -

pull - git clone syntax - java check syntax integrate - javac integrate compile - javac -o packaging - tar -xzf .jar

Continuous Integration Process -> Gitlab-ci, Jenkins, Bamboo, Github Action, AWS Code Pipeline, Azure Pipeline, Cloud Build, etc.

Deployment -> cp .jar /opt/tomcat/webapps/.jar Delivery -> aws cp .jar s3://my-bucket/.jar

Continuous Testing

Continuous Deployment OR Delivery
Jenkins - Hudson company CICD java, 8080 root dir: /var/lib/jenkins

widqah-wIsveh-2xurje

Install Jenkins
install java
apt-get update
apt install fontconfig openjdk-17-jre -y
java -version
Install Jenkins
 wget -O /usr/share/keyrings/jenkins-keyring.asc   https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
 echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]"   https://pkg.jenkins.io/debian-stable binary/ | sudo tee   /etc/apt/sources.list.d/jenkins.list > /dev/null
 apt-get install jenkins
Start Jenkins
systemctl start jenkins
systemctl enable jenkins
Practical Summary
How to install Jenkins Server
Run your first job
New item
Build Step
How to install plugins
manage jenkins
plugins
available plugins
search plugin and install
Create master slave Jenkins
instance launch (on node)
java install (on node)
manage jenkins
node
new node
remote root dir /home/ubuntu
labels node
Launch Method - Launch via ssh - host - private IP credential - add key (user and private key) Host Key Verification Strategy - non
Job configure (restric node (label - node))
JOB - Github

Pipeline - Plugin suit Multistage JOB Declarative and Scripted Pipeline

Practical Summary
Parameterize job

Pull code from Github plugin: git SCM: github url

Pipeline Plugin: pipeline, pipeline: Stage view Create Pipeline Job pipeline { agent any stages { stage('Build') { steps { echo 'Hello World' } } stage('Test') { steps {

     }
 }
 stage('Deploy') { 
     steps {
         
     }
 }
} }

Pipeline:
Java based - Angular - maven

Pull - Git Clone repo Build (.war / .jar) - Syntax, integrate, compile, package Test (Sonarqube) - test Deploy (tomcat / Java) - cp .war /tomcat/webapps/

Maven - Automate Build Tool

syntax, integrate, compile, run, test, packaging

Install maven Create project Studentapp(java, maven) - student.war

Maven lifecycle
default () clean site

mvn clean package

Quality Analysis:

Sonarqube

Vulnerability (Security Risk) Code Smell Duplications Bugs

Java 9000

8d01d22907dd53f5d74e51ab4648ae4269524141

Deploy
Server (TOMCAT) S3 - Versioning Docker image - ECR Kubernetes cluster - EKS

Plugin: Deploy to container

stage('Deploy') { steps { sh '''docker build . docker push ecr.io/image:latest''' } } stage('Deploy') { steps { sh '''aws s3 cp targets/*.war bucket:/''' } } stage('Deploy') { steps { sh '''docker build . docker push ecr.io/image:latest kubectl apply . ''' } }

SED AWK

yum install httpd -y systemctl start httpd systemctl enable httpd cp ./index.html /var/www/html/



*********************************************************************************************************

# SonarQube Installation

## Prerequisites
- SonarQube server will require 3GB+ RAM to work effeciently

### Install Database
```shell
rpm -ivh http://repo.mysql.com/mysql57-community-release-el7.rpm
rpm --import https://repo.mysql.com/RPM-GPG-KEY-mysql-2022
yum install mysql-server -y
systemctl start mysqld
systemctl enable mysqld
grep 'temporary password' /var/log/mysqld.log
mysql_secure_installation
```

### Install Java
```shell
yum install wget epel-release -y
yum install java -y
wget https://download.bell-sw.com/java/11.0.4/bellsoft-jdk11.0.4-linux-amd64.rpm
rpm -ivh bellsoft-jdk11.0.4-linux-amd64.rpm
#alternatives --config java
```

### Configure Linux System for Sonarqube
```shell
echo 'vm.max_map_count=262144' >/etc/sysctl.conf
sysctl -p
echo '* - nofile 80000' >>/etc/security/limits.conf
sed -i -e '/query_cache_size/ d' -e '$ a query_cache_size = 15M' /etc/my.cnf
systemctl restart mysqld
```
### Configure Database for Sonarqube
```shell
mysql -p -u root
mysql>
    create database sonarqube;
    create user 'sonarqube'@'localhost' identified by 'Redhat@123';
    grant all privileges on sonarqube.* to 'sonarqube'@'localhost';
    flush privileges;
```
### Install Sonarqube
```shell
yum install unzip -y
wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-7.9.1.zip
cd /opt
unzip ~/sonarqube-7.9.1.zip
mv sonarqube-7.9.1 sonar
```
### Configure Sonarqube
```shell
sed -i -e '/^sonar.jdbc.username/ d' -e '/^sonar.jdbc.password/ d' -e '/^sonar.jdbc.url/ d' -e '/^sonar.web.host/ d' -e '/^sonar.web.port/ d' /opt/sonar/conf/sonar.properties
sed -i -e '/#sonar.jdbc.username/ a sonar.jdbc.username=sonarqube' -e '/#sonar.jdbc.password/ a sonar.jdbc.password=Redhat@123' -e '/InnoDB/ a sonar.jdbc.url=jdbc.mysql://localhost:3306/sonarqube?useUnicode=true&characterEncoding=utf&rewriteBatchedStatements=true&useConfigs=maxPerformance' -e '/#sonar.web.host/ a sonar.web.host=0.0.0.0' /opt/sonar/conf/sonar.properties
useradd sonar
chown sonar:sonar /opt/sonar/ -R
sed -i -e '/^#RUN_AS_USER/ c RUN_AS_USER=sonarqube' sonar.sh
```
### Start Sonarqube
```shell
/opt/sonar/bin/linux*/sonar.sh start
/opt/sonar/bin/linux*/sonar.sh status
/opt/sonar/logs
```


6c387f93b2f66e644f55a697941b16c9b71cee29
hyxwyb-1sufpi-vaNdad

mvn sonar:sonar \
  -Dsonar.projectKey=studentapp \
  -Dsonar.host.url=http://18.234.80.25:9000 \
  -Dsonar.login=6c387f93b2f66e644f55a697941b16c9b71cee29

What is Sonarqube?
Creating sonarqube.
Sonarqube IAM 
Sonarqube testing

bugs, vulnerabilities, code smell, duplications
---
Pipeline - sonarqube


Pipeline
---------

Code File > Syntax Test > Compile > Run > Package > test > Deploy



Code > Build > Test > Deploy

CI-CD


Git pull origin main
mvn clean package
mvn sonar:sonar
cp webapps


Bash Scripting
Jenkins 