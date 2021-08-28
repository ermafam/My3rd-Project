# My3rd-Project

# PROJECT 3: MERN STACK IMPLEMENTATION


In this project, you are tasked to implement a web solution based on **MERN** stack in AWS Cloud.

**MERN** Web stack consists of following components:

1. **MongoDB:** A document-based, No-SQL database used to store application data in a form of documents.

2. **ExpressJS:** A server side Web Application framework for Node.js.

3. **ReactJS:** A frontend framework developed by Facebook. It is based on JavaScript, used to build User Interface (UI) components.

4. **Node.js:** A JavaScript runtime environment. It is used to run JavaScript on a machine rather than in a browser.


![image](https://user-images.githubusercontent.com/84423958/131227137-049cdeb7-1f67-463d-bce2-7cada75ec9d2.png)


As shown on the illustration above, a user interacts with the ReactJS UI components at the application front-end residing in the browser. This frontend is served by the application backend residing in a server, through ExpressJS running on top of NodeJS.

Any interaction that causes a data change request is sent to the NodeJS based Express server, which grabs data from the MongoDB database if required, and returns the data to the frontend of the application, which is then presented to the user.

## Side Self Study

1. Make a research what types of **Database Management Systems (DBMS) exist and what each type is more suitable for**. Be able to explain the difference between Relational DBMS and  
   NoSQL (of a different kind).
2. Get yourself familiar with a concept of **Web Application Frameworks**. Get to know what server-side (backend) and client-side (forntend) frameworks exist and what they are used 
   for
3. **Practice basic JavaScript syntax just for fun.
4. Explore what **RESTful API** is and what it is used for in Web development.
5. Read what **Cascading Style Sheets (CSS)** is used for and browse **basic syntax and properties**.
Instructions On How To Submit Your Work For Review And Feedback
To submit your work for review and feedback – follow **this instruction.

Step 0 – Preparing prerequisites
In order to complete this project you will need an AWS account and a virtual server with Ubuntu Server OS.

If you do not have an AWS account – go back to **Project 1 Step 0** to sign in to AWS free tier account and create a new EC2 Instance of t2.nano family with Ubuntu Server 20.04 LTS (HVM) image. Remember, you can have multiple EC2 instances, but make sure you **STOP** the ones you are not working with at the moment to save available free hours.

**Hint #1:** When you create your EC2 Instances, you can add Tag "Name" to it with a value that corresponds to a current project you are working on – it will be reflected in the name of the EC2 Instance. Like this:


![image](https://user-images.githubusercontent.com/84423958/131227472-383845d9-91dd-43da-b4c4-ebe5fa042afc.png)


**Hint #2 (for Windows users only):** In previous projects we used Putty and Git Bash to connect to our EC2 Instances. For Windows, there is a tool you can use to open multiple tabs of your CLI in a single window.

**MobaXterm** is an advanced multirotocol and multitool terminal for Windows.

Download and launch MobaxTerm, create a new SSH session with , ‘ubuntu’ as username and your private key (.pem file) like this:


![image](https://user-images.githubusercontent.com/84423958/131227586-96f515dc-f8ab-4f69-8035-0202c1b1444b.png)


To deploy a simple **To-Do** application that creates To-Do lists like this:



![image](https://user-images.githubusercontent.com/84423958/131227648-311a9e0e-083f-40ee-9179-49b86f4693e0.png)


## STEP 1 – BACKEND CONFIGURATION


Step 1 – Backend configuration

Update ubuntu

```
sudo apt update
```

Upgrade ubuntu

sudo apt upgrade


Lets get the location of Node.js software from **Ubuntu repositories.


```

curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -

```

**Install Node.js on the server

Install Node.js with the command below

```
sudo apt-get install -y nodejs
```

**Note**: The command above installs both **nodejs** and **npm.** **NPM** is a package manager for Node like **apt** for Ubuntu, it is used to install Node modules & packages and to manage dependency conflicts.

Verify the node installation with the command below

```
node -v 
```

Verify the node installation with the command below

```
npm -v 
```

**Application Code Setup

Create a new directory for your To-Do project:

```
mkdir Todo
```

Run the command below to verify that the Todo directory is created with ls command

```
ls
```

**TIP:** In order to see some more useful information about files and directories, you can use following combination of keys **ls -lih** – it will show you different properties and size in human readable format. You can learn more about different useful keys for**ls** command with **ls --help.

Now change your current directory to the newly created one:

```
cd Todo
```

Next, you will use the command **npm init** to initialise your project, so that a new file named **package.json** will be created. This file will normally contain information about your application and the dependencies that it needs to run. Follow the prompts after running the command. You can press **Enter** several times to accept default values, then accept to write out the package.json file by typing **yes.



![image](https://user-images.githubusercontent.com/84423958/131228500-4129f6b1-96b8-46bb-851c-1d06151f4a43.png)


