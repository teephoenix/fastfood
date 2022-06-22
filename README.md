# fastfood
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



## Start BackEnd : datasourse

1. install MySQL Database
2. config the MySQL datasource in the application.properties file (Datasource URL, Database name and password)

## Start BackEnd : Java and Tomcat

1. instal JDK 8, and Apache Maven 3.6.3
2. go to the __fastfood_BackEnd__ folder, then compile the project : __mvn clean package__
3. start the back-end project : __java -jar target/fastfood-0.0.1-SNAPSHOT.jar__


## Start FrontEND : This project was generated with Angular CLI version 10.0.5.

1. go to the __fastfood_FrontEnd__ folder, then Install Nodejs and npm
2. make these commands : 
- install angular cli : __npm install -g @angular/cli@10.0.5__
- install all module : __npm install --force__
- start the application server : __ng serve__

3. open the browser and make this url to start __FrontEnd__ : http://localhost:4200

## some ionformation for the connection : 

1. utrains@utrains.test | Role : Admin    | pwd : Utrains_p@ss
2. alain@utrains.test   | Role : Customer | pwd : Alain_p@ss
