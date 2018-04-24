# Assignment Deployment Checklist:

This document is meant to be a checklist helpful to students when they are ready to deploy their assignments to Digital Ocean.
It covers and consolidates the basics of deployment for typical projects required in the course. If your application includes variations or 
additions your procedures may involve different steps.

__Conventions in this document:__
  * *C:\local$* is used to represent the Cmdr Command Line '$' prompt for the LOCAL development machine.
  * *X:\ocean#* is used to represent the Cmdr Command Line prompt when ssh'd into the Digital Ocean droplet.
  * *[IP]* represents a numeric IP address. (Example, the IP address of localhost is numeric IP *127.0.0.1*)
  * *[port]* represents a numeric port number. (Example, you may use port number *8080*)
  * So the following: *[IP]:[port]* might represent *127.0.0.1:8080*

__Assumptions: the student already has:__
  - Their own github account
  - A Digital Ocean droplet and knows their droplet's IP address
  - Followed the steps for setting up the SSH keys between github and the Digital Ocean server as noted in the course module.
  - Cloned the assignment to their local machine from the git repo provided, and created an app to deploy

## BEFORE DEPLOYING: Getting ready to deploy your assignment:

1. Start your Cmdr Command Line tool.

2. In Command Line, change to the working directory where your assignment is located:
  - *C:\local$*`cd assignment-X`      // you may be nested several levels, such as C:\users\uname\cscie31\assignmentX

3. Double check your files:

- Have you updated your project Readme file?
- Is your package.json file up to date?           // If package.json has not been discussed in lectures, skip this check - it may not apply.
- Do you have a .gitignore file? Is it correct?   // To exclude some files from your git repository. If not yet discussed in lecture, skip this or ask TA.
- Have you checked in your files? **Check In** is outlined in the next step.

4. Check In your code to Github:  In Cmdr, in the directory for your application:

- Run git status:                           
    - *C:\local$*`git status`
- Based on status, add files to your repo:  
    - *C:\local$*`git add --all`  // adds all changes reported by git status. (You can add/remove files selectively if you prefer)
- Commit the changes you added:             
    - *C:\local$*`git commit -m "Make a comment about the changes"` //(You can also do this for individual files if you prefer)
- Send your sources to your github repository:    
    - *C:\local$*`git push origin master` // push the changes to github.

5. Now you are ready to pull your project to your Digital Ocean droplet.

## DEPLOYMENT STEPS: Deploying your assignment to Digital Ocean:

1. From the Cmdr Command Line tool ** *ssh* ** into Digital Ocean using your droplet's IP address.

* *C:\local$*`ssh root@[IP]`

2. Clone your assignment repository. Go to Github and select the repository to clone. From the 'Clone or Download' button, copy the SSH Setting. Example:

* *X:\ocean#*`git@github.com:HarvardDCENode/assignment-X-name.git`

3. Open the port you use for the assignment so the server will allow access. If you used that port number for a previous assignment this may not need to be not be repeated. If you have another assignment app that is still listening on that port, you may need to open another port.

- *X:\ocean#*`sudo ufw allow 8080`

4. Clone your github repository to your Digital Ocean droplet which will copy your files from github to your droplet. ?????????????????????????ADD HOW TO GET CLONE STRING?

- *X:\ocean#*`git clone https://github.com/assignment-X-description-yourname.git`

5. Navigate to your assignment directory:

-*X:\ocean#*`cd assignment-X-description-yourname`  // where assignment-X... is the name of your folder.

## Starting your Application:

From here, how you complete setting up and starting your project will vary depending on how far you are in the course.

### For your introductory Node server 

// T start for initial testing:
-*X:\ocean#*`node appserver`  // where appserver.js is the name of the server file. YOU MUST NOT CLOSE YOUR Cmdr TOOL in order to try accessing the server. Closing Cmdr will cause appserver to halt.

// To leave your server running when you close your Cmdr tool:
-*X:\ocean#*`nohup node appserver &`    // Now you and your grader can access the server at any time, without using Cmdr.

// Visit your web server through a browser:
http://[IP]:[port]

### For a basic web app using Node modules and NPM packages:

Follow the Deployment steps through Step #5. Then:

6. Install your NPM packages:

-*X:\ocean#*`npm install`       // Uses the package.json file to install Node modules / NPM packages and their dependencies on your Digital Ocean droplet.

// Start your server in the same way as you did for your introductory Node server, and visit via a browser in the same way:
-*X:\ocean#*`nohup node appserver &` // where appserver.js is the name of the server file.


### For a web app using Express and Package.json Scripts:

Follow the deployment steps as outlined above. The difference will be in how you start your deployed server:

-*X:\ocean#*`nohup node start &` // where 'start' is the name of your script. You won't use your development script because nodemon is a tool for the development environment


### For a web app that uses MongoDB, Mongoose, and dotenv:

It is not much more complicated to set up this project, but some confusion can arise. 
- First, you will usually not want to expose your database username and password publicly in your github repository, so take steps in the early part of the process to prevent that. Hint: `.gitignore`, `.env` file. 
- Second, Mongoose and dotenv are NPM modules, and are handled the same way you dealt with others. Hint: `npm install`. 
- Third, your database is in the 'cloud'. It is not necessary to install any of the database client side software tools (Compass, the MongoDB shell) on Digital Ocean. Mongoose is going to handle the database interaction from DO, the same way that it does from your local development project. If you want to create a new database for 'production' purposes, you can set all of that up, and initialize it with data, from your local machine. You will can modify your connection string to connect to the production database, but you can gry that from localhost before you deploy your code.

Follow the steps as outlined for other projects. Then:

7. Create a .env file to use for your db credentials. In your Cmdr shell, use the editor Nano:

-*X:\ocean#*`nano .env` // brings up the nano code editor
 
- Type in the same lines as you have in your local .env file, with *your* values for username and passworX:
```
DB_USER=username
DB_PWD=password
```

- Then enter Crtl-X and you will be prompted whether to Save. Click Y for yes. Then you will be prompted for the file name, which will default to .env because of your 'nano .env' entry, so press return.

Start your server as before:
-*X:\ocean#*`nohup node start &`

==============================================TROUBLE SHOOTING:============================
Ports: Type (or paste) sudo ufw allow 8080 to open port 8080 for serving http.  (For a port conflict, say, your old app is still running using that port)

Update DO: with git pull origin master
