# Assignment checklist:

This document is meant to be a checklist helpful to students when they are ready to deploy their assignments to Digital Ocean.

__Convention:__
  * *C:\local$* is used to represent the Cmdr Command Line '$' prompt for the LOCAL development machine.
  * *X:\ocean$* is used to represent the Cmdr Command Line '$' prompt when ssh'd into the Digital Ocean droplet.

__Assumptions: Student has:__
  - Cloned the assignment from the git repo provided, and created an app to deploy
  - Their own github account
  - A Digital Ocean droplet

__Getting ready to deploy your assignment:__

1. Start your Cmdr Command Line tool.
2. Move to your working directory where your assignment is located:
  - *C:\local$*`cd assignment-X`      // often you may be nested several levels, such as C:\users\uname\cscie31\assignmentX

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
