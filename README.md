# Download and Install
The first thing you need to do is to download some software that we will be using for the course. Please note that I should be able to help with installation on PCs, but less so with Apple devices.
## Text Editor
   This is not an absolute requirement because most operating system have a built in text editor. That said, I have found Notepad ++ to be quite useful because it will allow you to write text in just about any language (html, markdown, plain, etc.) and will recognize the format. There are also lots of plugins that you can add depending on what you do.  
   [Download Notepad++](https://notepad-plus-plus.org/downloads/)
## Git
   The next program we will download is Git. This is a version control software and is used to help keep track of changes that are made when you are writing a paper or writing code for a program or project. The idea behind version control is like a library where you can store the main information on the cloud and then update what is there when you have made changes that you want to keep. Another key feature is that it keeps a record of each time you submit changes so you can go back, or revert, to any previous version of a project.  
   [Download Git](https://gitforwindows.org/)
## R Core
   The next thing you will need is to install the core R program. R is a free programing language that you can use for pretty much anything and is along the lines of Python. The core R program has many capabilities, however, the real power comes from the packages or "libraries" that you can add to the software. These are created by other users and are typically specialized for specific tasks ranging from web scraping to simple regressions.  
   [Download Core R for Windows](https://cran.r-project.org/bin/windows/base/)  
   [Download Core R for iOS](https://cran.r-project.org/bin/macosx/)
## R Studio
   The last thing we will download is going to be R Studio and it is going to be our workhorse. In short, it is a graphical user interface (GUI) that allows us to access Core R, libraries we download, version control, and many other aspects of a project all in one place. It is even possible to write an entire paper within R Studio and, most importantly, it is free.  
   [Download R Studio](https://posit.co/download/rstudio-desktop/) *Scroll down for various operating system downloads.*

## U.S. Census API Key
   We will be using a service of the U.S. Census Bureau known as an API and this requires obtaining an API Key. This is free and simply a means of keeping tabs on who is accessing the database for what use. To obtain a key, go to the [Census Key Website](https://api.census.gov/data/key_signup.html) and fill in your name, email address (really should use your z-id email address) and agree to the terms of service. Your key will now be sent to you in your email account. Make sure to save this email, because we will be using it in class.
# Setup and Configuration
Now that everything is installed, open your RStudio program and you should see a screen that looks something like this:
![[Pasted image 20251031124157.png]]
While not necessary, we will do just about everything we need to do to get setup in the RStudio interface. Specifically we will set up our GIT identification and set up our working directory structure.
## GIT Identification
To use `GIT`, you need to identify yourself so that when we commit changes, we can know *who* made those changes. We will do this using the RStudio terminal which is a command line based shell. Other options are to use `GIT Bash` which you installed when you installed GIT on your machine, or your operating systems own terminal or command line system. For us, notice in the top left window of RStudio we see three tabs: Console, Terminal, and Background Jobs.  You will need to click on Terminal to access the shell program. Once that window has popped up, you are given the command prompt where you need to input the two lines of command. Use your own name and email address that corresponds to your GitHub account.

```bash
git config --global user.name "Jeremy R. Groves"
git config --global user.email "jgroves@niu.edu"
```
This will now tag all of your `GIT` work with your name and email so that we can make sure we know who has submitted what changes.
## R-Studio and Git/GitHub
Next we want to link `R Studio` with `Git` and allow it to access GitHub securely. We do not have to use `R Studio` to utilize the feature of Git or GitHub because we can use the command line prompts (Git Bash) for that as well. Since `RStudio` provides a standard means of interacting with `R`, especially for novice users, we will continue to use this. With `RStudio` still open, go to the menu across the top of the screen and locate `TOOLS --> GLOBAL OPTIONS` and a smaller screen will open. Along the left side, click on the part that states `GIT/SVN` and then make sure the box at the top is checked and then in the area below "Git Executable" you need to navigate to the `git.exe` file. On a PC, it will be located at `C:/Program Files/Git/bin/git.exe`. You can either type this address in or you can navigate to it via the Browse button. Once this box is filled in, click Apply and then Okay.
![[Pasted image 20251031125617.png]]
Next, we need to allow GitHub and `R Studio` to talk to each other securely and for that we need a personal passkey. Fortunately someone wrote a library and program in `R` for just that purpose. Since we are not going to download the full library with these commands in them, we can use the `usethis::` command prefix and then use the command `create_github_token()`. To run the necessary code, choose the Console option of the three tab in the left-side window of `RStudio` and type each of the lines of code below following each with the ENTER key.

```R
install.packages("usethis")
usethis::create_github_token()
```

After the second command, GitHub should open on your browser and ask you to log in. Once you do that, you should see the following screen.
![[Pasted image 20251031125925.png]]
You can name your passkey whatever you want and then click on the drop-down menu and choose at least 90 Days (this will get us through the class). Scroll to the bottom and click **Generate Token** and you will get a sting of letters and numbers. This is Hexadecimal text and make sure to copy this and then paste it either in a Word file or a text file because once you close this window, you will NEVER get this token back. If you lose it; however, you can just generate a new one and use it. Once you have copied the code somewhere else, go back to `RStudio` and then type the following in the console.

```R
gitcreds::gitcreds_set()
```

You should see a set of options and you should choose `2` and then when it asks for the token, paste the hexadecimal code you copied and press enter. This will save the passkey in the R system files and you will only need to do this again if your code expires or, sometimes, when you update R.  
## R Library Setup (optional)
`R` is a solid program for data analysis; however, most of its power comes in its ability to use libraries. These are add-ons created by other users that expand what the program can do or simplify the way a script is written. Most of these packages are located at the CRAN website; however, others can be found on GitHub. To use them, they must first be downloaded and then installed into `R`. Another aspect of how `R` works is that when the base `R` is updated and you install the new version, it DOES NOT overwrite the previous version, rather it installs the new version along side the older version. The reason for this is that some of the libraries fall out of use and are not updated for new `R` versions and so having an older version allows users to access those tools. The tradeoff to this system is that the libraries are installed in the version specific folder so when you update `R`, you must also reinstall all libraries. Since we do not typically run into the version problem, it becomes helpful to place all of your libraries into one common directory and then just update where `R` looks for the library files.  

To make this change, we first need to find the `Rprofile.R` file on your computers. For PC users you can find this file at `C:/Program Files/R/*current install*/library/base/R`. Navigate here using your file explorer program and then find the file `Rprofile.R` and right-click and choose to edit with **Notepad++** or other text editor. When it opens, scroll all the way down to the bottom and then add the following text. 

```R
#My Stuff
myPaths <- c("C:/Users/.../Documents/R/userLibrary", .libPaths())
.libPaths(myPaths)
```

Within this code, the command `.libPaths()` holds the location of where `R` looks for library files when you use the `library()` command in your script. This code updates that object by adding the user defined library location. My listing this one first, it also designates our user defined library as the default location when we install libraries for `R` to use. By placing this command in the `Rprofile.R` script, which is a script `R` runs on start up, we are always updating this variable every time we start up `R`. 
## Installing and Using Libraries

Now lets go ahead and install a couple of libraries by opening `R Studio` and looking in the window on the left side and making sure you are in the Console tab. This is where you can run "command line" code to `R` without a script. While not ideal for working on projects, it is fine for quick set-ups or function calls. 

You have actually already done this when you installed the *usethis* package above. This time, however, we will install one of the power-house packages we will be using *tidyverse*.  *Tidyverse* is a package which is a collection of several packages that make getting, cleaning, manipulating, and visualizing data of various types (numbers, character strings, dates, etc.) much easier and intuitive. Try to install this package on your own, but if you struggle, here is the code.
```R
install.packages("tidyverse")
```
## Project Management and GitHub

Whether you are by yourself, working with a team, or, more to your cases, working with an advisor, having an effective "project" setup will help you organize your thoughts and ideas and provide an much easier way to interact with an advisor or co-author. While `RStudio` has a built-in project system, we are going use this in conjunction with `GitHub` to ensure there is always a copy of our information we can get to if needed. This is ideal if you are working across multiple devices and locations. 

Organization also helps you work with others and remember what you did and why when you revisit a project either an hour or a year after you started it. Organization also helps you should you need to prove or verify your work either to a professor or a journal when you submit for publication. This later issue, that of reproducibility, is becoming even more important given the number of cases of academic misconduct being uncovered, even among Nobel Prize winners. We are going to organize our project in `RStudio` and then back it up in a `GitHub` Repository for both protection and for easier remote access by ourselves or co-workers. We start the process in reverse however.
### Create Repository on GitHub
A Repository is a place on the GitHub cloud where you can keep relevant files for any given project. You have each setup a profile on `GitHub` and are all part of the GitHub Classroom environment for this class. Use this URL link (https://classroom.github.com/a/aYMYVjZ6Go) to get to the `Groves R` Repo to check it out and clone a local copy in your `GitHub` account. From your own `GitHub` account, go to this repository and copy the URL line in the browser window or using the down-arrow of the green CODE button in `GitHub`. 
### Create Project in R-Studio
As mentioned, `RStudio` has a system built into it that acts as a means for keeping information and data on a project together called *PROJECTS*. We can create a project on our computer only, or we can link it to a GitHub or similar type repository. Creating projects, however, is of little use if we do not know where we left them so I recommend that you create a **Projects** directory in your systems **My Documents** folder (or its Apple equivalent)

Next we will return to the drop-down arrow in the upper-right corner of our `RStudio` windows that says **PROJECT(none)**. Click on this and choose "New Project". A small screen will open on your computer and you need to click the Version Control banner and then click on the Git banner.  
<p align="center">
  <img src="https://github.com/jrgroves/ECON691/assets/52717006/64332c4b-b877-40b7-bc5b-a5c91569ecc3"/>
</p>
The window that is now open is asking for the URL from the repository that you created on `GitHub` which you can get by simply navigating to the repository in your web browser and copy the URL from the location bar at the top of the browser. Once copied, you can paste in the URL space and that will typically auto populate the Project Name dialog box below it. The third box is were it will live on your computer and if not already showing your **Projects** directory, click the browse button and navigate to that directory. Once you are there and click open, click the "Create Project" button on the screen.  
<p align="center">
  <img src="https://github.com/jrgroves/ECON691/assets/52717006/6a2e5628-6035-4016-9ab1-997a0459726a"/>
</p>
Once you hit "Create Project" it will appear that `RStudio` reloads and we will be ready to start working. The other action you will notice is that a copy of the `Groves R` repo that you cloned to your `GitHub` account is now going to be copied, or cloned, to your device. You can verify this by looking at the *Files* tab in the lower-right side of `RStudio` and notice that it now switches to a newly created directory within your **Projects** directory with the same name as your repo on GitHub and sets the working directory in `R` to that location. To verify this, type the `getwd()` in the console and see what is reported.  The last thing you should notice that is different is that there is now a new tab in the upper-right window of `RStudio` called *Git*. Under this tab is one way we can interact with both `Git` and GitHub.
## Your First Push
Version control allows us to keep track of changes both by us and anyone else that has permission to access our repository. It does not, however, keep track of all of our key strokes and it can only track what we tell it to track and it takes a "snapshot" only when we tell it to. Whenever we create or modify a file, version control, or in this case `Git`, will recognize that it is different than what is currently in the repository, but that is the extent of what it will do on its own. We we complete our modifications and want to update what we have on our main or branch, we must first "stage" the files. 

We can stage as many files as we want and we can think of "staging" as placing our newly changed files in an envelop that we are going to "mail" to our repo. To actually submit the changes so that version control will commit them to "memory", we have to commit them. When we commit a set of changes, we have the option to add a comment to our commit to tell ourselves or others what we changed in this part that is being committed. Once we commit, version control creates a new "version" of the project using those files and creates a history which contains the older versions of our project prior to those changes that were committed.

To practice this in our example, we are going to create a text file to tract what we do each day in class. In `RStudio`, use the `FILE--->New File--->Markdown File` and this will split the left-side of your screen as the Editor is opened. The Console will slide to the bottom and you will be able to edit documents and scripts in the upper frame. Type something similar to the following into this space. 
```
# Tracking for Economics 691 Projects
Today we installed our software, set up a project, and tried our first GitHub Push.
```
Once that is completed, click on the disk icon and save the file as **Tracking** and you can simply save it in your current directory (which should be your project directory). Once the file is saved, go to the upper-right window and click on the GIT tab. You will see a list of files there that you can choose to "stage" so look for the newly created **Tracking** file. You should see an empty checkbox and two yellow squares to the left of the file name. Once you click the checkbox, the two yellow will become one green with the letter 'A' in the box. This means the file is "staged." If you had modified a file already part of the repository, you would see the empty checkbox and a blue square indicating it has been modified and not committed. 

We want to commit our Tracking file to the repository so after we click the checkbox and see the green box, we click on the COMMIT button near the top of this GIT tab. That will open a new window and all we want to is type something the upper-right window. This is our commit message to remind us later what we committed this time. Type something like "initial commit" and then click the COMMIT button. A status window will pop up and you can click CLOSE once it is finished. You can then exit out of the other window that is open (where you put your commit message) and return to the GIT tab. 

At this point, the file is committed to the version of our repository on your device, but not at `GitHub`. You can verify this by looking at the repo in your browser. Returning to `RStudio` and the GIT tab, you will see a button that says PUSH. Click this and the version of the repository on your device will be "pushed" up to the cloud. Once the status windows indicates it is finish, return to your browser and refresh and you should now see your Tracking file in your directory online. Congratulations, you just pushed your first commit. 
