# Assignment checklist:

This document is meant to be a checklist helpful to students when they are ready to deploy their assignments to Digital Ocean.

__Convention:__
  * *C:\local$* is used to represent the Cmdr Command Line '$' prompt for the LOCAL development machine.
  * *X:\ocean#* is used to represent the Cmdr Command Line prompt when ssh'd into the Digital Ocean droplet.
  * *<IP>* represents a numeric IP address. (Example, the IP address of localhost is numeric IP *127.0.0.1*)
  * *<port>* represents a numeric port number. (Example, you may use port number *8080*)
  * So the following: *<IP>:<port>* might represent *127.0.0.1:8080*

__Assumptions: the student already has:__
  - Cloned the assignment from the git repo provided, and created an app to deploy
  - Their own github account
  - A Digital Ocean droplet and knows their droplet's IP address
  - Followed the steps for setting up the SSH keys between github and the Digital Ocean server as noted in the course module.

## Getting ready to deploy your assignment:

1. Start your Cmdr Command Line tool.
2. Move to your working directory where your assignment is located:
  - *C:\local$*`cd assignment-X`      // you may be nested several levels, such as C:\users\uname\cscie31\assignmentX

3. Check your files:

  - Is your package.json file up to date?
  - Do you have a .gitignore file? Is it correct?  // You may want to exclude some files from your git repository
  - Have you checked in your files? See next step.

4. Check in your code:  In Cmdr, in the directory for your application:

- Run git status:                           *C:\local$*`git status`
- Based on status, add files to your repo:  *C:\local$*`git add --all` // adds all changes reported by git status. (You can add/remove files selectively if you prefer)
- Commit the changes you added:             *C:\local$*`git commit -m "Make a comment about the changes"` (You can also do this for individual files if you prefer)
- Send changes files to your github repo:   *C:\local$*`git push origin master` // push the changes to your github repository.

5. Now you are ready to pull your project to your Digital Ocean droplet.

## Deploying your assignment to Digital Ocean:

1. From the Cmdr Command Line tool *ssh* into Digital Ocean using your droplet's IP address.

-*C:\local$*`ssh root@<IP>`

2. Clone your assignment repository. Go to Github and select the repository to clone. From the 'Clone or Download' button, copy the SSH Setting. Example:

-*D:\ocean#*`git@github.com:HarvardDCENode/assignment-X-name.git`

3. Open the port you use for the assignment so the server will allow access. If you used that port number for a previous assignment this may not need to be not be repeated. (Note that if another assignment app is listening on that port and it is still running, you may need to open a different port.)

-*D:\ocean#*`sudo ufw allow 8080`

4. Clone your github repository to your Digital Ocean droplet which will copy your files from github to your droplet. (On Github, ????????????????????)

-*D:\ocean#*`git clone https://github.com/assignment-X-description-yourname.git`

5. Navigate to your assignment directory:

-*D:\ocean#*`cd assignment-X-description-yourname`  // where assignment-X... is the name of your folder.
(You can copy the folder name by running the `ls` command. Select (swipe) the name of the folder with your mouse. Move back to the prompt and insert with the 'Paste' key combination, Shift-Insert for Windows.)

## Starting your Application:

From here, how you complete setting up and starting your project will vary depending on how far you are in the course.

### For your introductory Node server 

// For testing:
-*D:\ocean#*`node appserver`  // where appserver.js is the name of the server file. YOU MUST NOT CLOSE YOUR Cmdr TOOL in order to try accessing the server. Closing Cmdr will cause appserver to halt.

// To leave your server running when you close your Cmdr tool:
-*D:\ocean#*`nohup node appserver &`    // Now you and your grader can access the server at any time, without using Cmdr.

// Visit your web server through a browser:
http://\<IP\>:\<port\>






==============================================
Ports: Type (or paste) sudo ufw allow 8080 to open port 8080 for serving http.  
