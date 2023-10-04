# fastfoodapp
### fast food application project using micro-services

This web-app is helpful to display various services, food items offered at each branch separately where Admins can add,edit and remove the food items for their specific branches and Customers can search,sort & filter the food items and order the food online & track the placed orders.

This is a Full-Stack Web Project done by using the Technologies- Angular (HTML, CSS & Type Script) for Frontend; SPRING Boot as Middleware; JAVA, Data JPA for Backend and MySQL Database. Software used :  Visual Studio Code for Frontend, Intellij for Backend and MySQL DB.

# App Description 
This application is a __3-tier__ application where we have : 
1. a frontend : developed with __Angular__
2. a backend : developed with Java and __Spring Boot__
3. a database : __MySQL__. 

## Deployement Process
We can deploy this application in 3 different ways: deployment on a Centos 7 server, deployment with Docker, and deployment with Docker-Compose.

### Note : use a server with at least 2GB of RAM


# 1- Deploy FastFoot App, using a single Centos 7 serveur
In the following description, we will give the main steps to deploy this application on a Centos 7 server. 

## Step 1 : Install git in the serveur 

In this step, we will : 
- connect to our Centos server
- update the server
- install git, 
- create a folder and enter this folder.
- clone the repository that contains the source codes of our application

```bash
  sudo yum update
  sudo yum update 
  sudo yum install git -y
  mkdir fastfood_deplyer
  cd fastfood_deplyer/
  git clone https://github.com/utrains/fastfood.git
```

## Stap 2 : configuring the database
In this step, we will install on our server, a MySQL database, create a database of our Application.
Here is the list of steps to follow to install MySQL on our Centos 7 server: 
1. We need to update our system
2. install wget
2. download the MySQL using wget
3. prepare the repository 
4. use __yum install__ command to install __MySQL__
5. Start MySQL and Check its Status
6. Configure MySQL and Changing MySQL Root User Password 

```bash
  sudo yum update
  sudo yum install wget -y
  sudo rpm -Uvh mysql80-community-release-el7-3.noarch.rpm
  sudo yum install mysql-server -y
  sudo rpm --import https://repo.mysql.com/RPM-GPG-KEY-mysql-2022
  sudo yum update -y
  sudo yum install mysql-server -y
  sudo systemctl start mysqld
  sudo systemctl status mysqld
  sudo grep 'password' /var/log/mysqld.log
```
```sudo grep 'password' /var/log/mysqld.log``` : this command will generate the temporary password for the root user of the database. 
- This password will allow us to change and set the root password of the root user of our application's database.
- Please note that for the configuration of our database, the developers have used the following configurations: 
1. user : __root__
2. password : __2j5R1HtsE7@mpM8Tdn92__
3. database name : __sandwitchdatabase__
- in the following commands, please change the password generated by the root user, by the password of our developer friends. 

```bash
    sudo mysql_secure_installation
```
- following this command, you will enter our developer password, then answer a few questions to validate the password change
- we will connect to MySQL with the user root, enter the password we just changed. 
- then create our database with the name that the developers specified in their configuration files

```bash
    mysql -u root -p
    SHOW DATABASES;
    CREATE DATABASE sandwitchdatabase;
```
Note : you can see the database config in the this file : [application config file](./fastfood_BackEnd/src/main/resources/application.properties)


## step 3 : compile and Start BackEnd 

1. install and configure the JDK 8 environment variable
2. install and configure the environment variable of __maven 3.8.5__
- download maven
- unzip the archive

```bash
    sudo yum install java-1.8.0-openjdk -y
    
    #--- install Maven 
    sudo -i 
    cd /opt
    wget https://dlcdn.apache.org/maven/maven-3/3.8.5/binaries/apache-maven-3.8.5-bin.tar.gz --no-check-certificate
    tar -xf apache-maven-3.8.5-bin.tar.gz
    rm -rf apache-maven-3.8.5-bin.tar.gz
    mv apache-maven-3.8.5/ maven
```
3. config these enviroment variable : __MAVEN_HOME__ and __JAVA_HOME__

```bash
    vim ~/.bash_profile
    M2_HOME=/opt/maven
    M2=$M2_HOME/bin
    PAHT=<Existing_PATH>:$M2_HOME:$M2
```

4. Compile and start the Backend : __The Sprint boot App__
```bash
    cd utrains_fastfood_repo/fastfood/fastfood_BackEnd
    mvn clean package
```
- a target folder is created and contains a __.jar__ file for the backend. run the command below to launch it.

```bash
    java -jar target/fastfood-0.0.1-SNAPSHOT.jar
```
- At this stage when everything is going well, you can connect to your database and see the information in it.


## Step 4 : Start FrontEND 
#### The frontend project was generated with Angular CLI version 10.0.5.

the steps of the node installation are the following:  
1. First, update the local repository 
2. Next, add the NodeSource repository 
3. install nodejs

```bash
    sudo yum update -y
    sudo yum install curl -y
    curl –sL https://rpm.nodesource.com/setup_10.x | sudo bash -
    sudo yum install –y nodejs
    node –version
```
#### enter the frontend folder and install the project dependencies using npm

1. go to the __fastfood_FrontEnd__ folder, then Install Nodejs and npm dependencies for the client

```bash
    cd utrains_fastfood_repo/fastfood/fastfood_FrontEnd
    npm install -g @angular/cli@10.0.5
    npm install --force
```

2. make this commands to start the frontend : 

```bash
    ng serve
```

3. open the browser and make this url to start __FrontEnd__ : http://localhost:4200

## some ionformation for the connection : 

1. utrains@utrains.test | Role : Admin    | pwd : Utrains_p@ss
2. alain@utrains.test   | Role : Customer | pwd : Alain_p@ss
