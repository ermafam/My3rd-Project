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

Run the command **ls** to confirm that you have package.json file created.

Next, we will Install **ExpressJs** and create the **Routes** directory.


## INSTALL EXPRESSJS

Install ExpressJS

Remember that Express is a framework for Node.js, therefore a lot of things developers would have programmed is already taken care of out of the box. Therefore it simplifies development, and abstracts a lot of low level details. For example, Express helps to define routes of your application based on HTTP methods and URLs.

To use express, install it using npm:

```
npm install express
```

Now create a file **index.js** with the command below

```
touch index.js
```

Run **ls** to confirm that your **index.js** file is successfully created

Install the **dotenv** module

```
npm install dotenv
```
Open the index.js file with the command below

```
vim index.js
```

Type the code below into it and save. Do not get overwhelmed by the code you see. For now, simply paste the code into the file.


```
const express = require('express');
require('dotenv').config();

const app = express();

const port = process.env.PORT || 5000;

app.use((req, res, next) => {
res.header("Access-Control-Allow-Origin", "\*");
res.header("Access-Control-Allow-Headers", "Origin, X-Requested-With, Content-Type, Accept");
next();
});

app.use((req, res, next) => {
res.send('Welcome to Express');
});

app.listen(port, () => {
console.log(`Server running on port ${port}`)
});
```

Notice that we have specified to use port **5000** in the code. This will be required later when we go on the browser.

Use **:w** to save in vim and use **:qa** to exit vim


Now it is time to start our server to see if it works. Open your terminal in the same directory as your index.js file and type:


```
node index.js
```

If every thing goes well, you should see **Server running on port 5000** in your terminal.


![image](https://user-images.githubusercontent.com/84423958/131228991-b6f5a699-50c3-41d3-8da2-c2653647ab7a.png)


Now we need to open this port in EC2 Security Groups. Refer to **Project 1 Step 1** – Installing the Nginx Web Server. There we created an inbound rule to open TCP port 80, you need to do the same for port 5000, like this:


![image](https://user-images.githubusercontent.com/84423958/131229006-ce29273d-be24-4d5f-8d76-cec413e0fb9a.png)


Open up your browser and try to access your server’s Public IP or Public DNS name followed by port 5000:


```
http://<PublicIP-or-PublicDNS>:5000
```

Quick reminder how to get your server’s Public IP and public DNS name:
1) You can find it in your AWS web console in EC2 details
2) Run **curl -s http://169.254.169.254/latest/meta-data/public-ipv4** for Public IP address or **curl -s http://169.254.169.254/latest/meta-data/public-hostname** for Public DNS name.

```
Welcome to Express
```

![image](https://user-images.githubusercontent.com/84423958/131229073-3bd01d6a-508a-4960-a24c-832d3e775d45.png)


**Routes

There are three actions that our To-Do application needs to be able to do:

1. Create a new task
2. Display list of all tasks
3. Delete a completed task
Each task will be associated with some particular endpoint and will use different standard HTTP **request methods:** POST, GET, DELETE.

For each task, we need to create **routes** that will define various endpoints that the **To-do** app will depend on. So let us create a folder **routes


```
mkdir routes
```

**Tip:** You can open multiple shells in Putty or Linux/Mac to connect to the same EC2

Change directory to **routes** folder.

```
cd routes
```

Now, create a file **api.js** with the command below

```
touch api.js
```

Open the file with the command below

```
vim api.js
```

Copy below code in the file. (Do not be overwhelmed with the code)


```
const express = require ('express');
const router = express.Router();

router.get('/todos', (req, res, next) => {

});

router.post('/todos', (req, res, next) => {

});

router.delete('/todos/:id', (req, res, next) => {

})

module.exports = router;
```

Moving forward let create **Models** directory.


## MODELS

Now comes the interesting part, since the app is going to make use of **Mongodb** which is a NoSQL database, we need to create a model.

A model is at the heart of JavaScript based applications, and it is what makes it interactive.

We will also use models to define the database schema . This is important so that we will be able to define the fields stored in each Mongodb document. **(Seems like a lot of information, but not to worry, everything will become clear to you over time. I promise!!!)

In essence, the Schema is a blueprint of how the database will be constructed, including other data fields that may not be required to be stored in the database. These are known as virtual properties

To create a Schema and a model, install **mongoose** which is a Node.js package that makes working with mongodb easier.

Change directory back Todo folder with **cd ..** and install Mongoose


```
npm install mongoose
```

Create a new folder with **mkdir models** command

Change directory into the newly created ‘models’ folder with **cd models.

Inside the models folder, create a file and name it **todo.js

```
touch todo.js
```

**Tip:** All three commands above can be defined in one line to be executed consequently with help of **&&** operator, like this:


```
mkdir models && cd models && touch todo.js
```

Open the file created with **vim todo.js** then paste the code below in the file:


```
const mongoose = require('mongoose');
const Schema = mongoose.Schema;

//create schema for todo
const TodoSchema = new Schema({
action: {
type: String,
required: [true, 'The todo text field is required']
}
})

//create model for todo
const Todo = mongoose.model('todo', TodoSchema);

module.exports = Todo;
```

Now we need to update our routes from the file **api.js** in ‘routes’ directory to make use of the new model.

In Routes directory, open **api.js with vim api.js**, delete the code inside with **:%d** command and paste there code below into it then save and exit

```
const express = require ('express');
const router = express.Router();
const Todo = require('../models/todo');

router.get('/todos', (req, res, next) => {

//this will return all the data, exposing only the id and action field to the client
Todo.find({}, 'action')
.then(data => res.json(data))
.catch(next)
});

router.post('/todos', (req, res, next) => {
if(req.body.action){
Todo.create(req.body)
.then(data => res.json(data))
.catch(next)
}else {
res.json({
error: "The input field is empty"
})
}
});

router.delete('/todos/:id', (req, res, next) => {
Todo.findOneAndDelete({"_id": req.params.id})
.then(data => res.json(data))
.catch(next)
})

module.exports = router;
```


The next piece of our application will be the **MongoDB Database



## MONGODB DATABASE

MongoDB Database

We need a database where we will store our data. For this we will make use of mLab. **mLab** provides MongoDB database as a service solution **(DBaaS),** so to make life easy, you will need to sign up for a shared clusters free account, which is ideal for our use case. Sign up here https://www.mongodb.com/atlas-signup-from-mlab. Follow the sign up process, select **AWS** as the cloud provider, and choose a region near you.

Complete a get started checklist as shown on the image below



![image](https://user-images.githubusercontent.com/84423958/131229885-25a5b93b-b355-40c1-bef8-08dc0a9b815a.png)
























