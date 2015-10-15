# Git (and Github) getting started guide

this guide walks trough the basic steps to start with source control. More specifically using git.
TFS, subversion, etc are concepts are very similar but one important note has to be made;
Git is a distrubuted source control system whereas for example TFS is a centralized source control repository.

The difference captured in an image
<insert image here>


# Let's get started
 first install Git and Github for desktop (Github for desktop includes all you need)
 
 ## Our first source controlled folder (getting started)

 First off, open the Git shell using the shortcut on the desktop. This is a powershell session host with git commands available.
  let's assume all our projects are stored locally on 'C:\<username>\Documents\My Projects' (and create the directory)
  
  ``` PowerShell
New-Item -ItemType Directory -Path $env:userprofile\Documents -Name 'My Projects' -force | Set-Location 
  ````
### initialize
To initialize our repository (or repo for short) we just need to type
```` bash
 git init Project01
````
 Git will return the following info:
 ``` bash
 Initialized empty Git repository in C:/Users/StijnCallebaut/Documents/My Projects/Project01/.git/
 ````
 This command actually created a hidden '.git' folder. the folder contains all the elements used to start tracking your project items.
 <insert image here>
 ### adding our first file
First we need a file, so let's create a file with some sample content
``` PowerShell
Get-Process | Out-File -FilePath .\OurFirstFile.txt
```
Notice that our prompt has changed. The prompt notifies us a file is added to our repo, but is not tracked yet.
To get a detailed status type:
``` PowerShell
  Git status
```
Output:
``` powershell
On branch master

Initial commit

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        OurFirstFile.txt

```
So let's stage our file and make it visible to our source control system   
``` PowerShell
Git add .\OurFirstFile.txt
```
 
 Note that adding the file does not actually add the file to our source control system. It merly makes it visible.
 It stages the file so it will be taken into account with possible other files (new or modified) when actually persisting (or commiting) it'
### Commiting the file
 Now that we have marked our file for staging, lets add commit it into the source control system.
 ``` PowerShell
 git commit -m 'This is the first file we will persist to our source control system'
 ```
 Git now saves a snapshot of the current state of our project folder.
 
## Remote repositories
 Until now we only worked locally and track those changes locally. This is already nice, but it does not enhance collaboration.
 So how can we start collaborating?
 
 ### Push our local repository to a remote location
 Now we will centrally store our Proejct01 on Github.
 To do so, we need to create a repo on Github, so log on to Github and create a new repository 'Project01'.
 Once the project is created, you can locate the git command and Github project01 repository url and copy the instructions
 <insert image >
 
 Back to our shell and execute the git commands
```PowerShell
git remote add origin https://github.com/Stijnc/Project01.git
```
Verify that the remote is added
```PowerShell
git remote -v
```
And push it
```PowerShell
git push origin master
``` 
### Clone an existing repository

If you want to get a copy of an existing Git repository � for example, a project you�d like to contribute to � the command you need is git clone. If you�re familiar with other VCS systems such as Subversion, you�ll notice that the command is "clone" and not "checkout". This is an important distinction � instead of getting just a working copy, Git receives a full copy of nearly all data that the server has. Every version of every file for the history of the project is pulled down by default when you run git clone. In fact, if your server disk gets corrupted, you can often use nearly any of the clones on any client to set the server back to the state it was in when it was cloned (you may lose some server-side hooks and such, but all the versioned data would be there � see Getting Git on a Server for more details).

You clone a repository with git clone [url]. For example, if you want to clone the Inovativ DemoProject, you can do so like this:
```PowerShell
 git clone https://github.com/Stijnc/DemoProject
```
That creates a directory named 'DemoProject', initializes a .git directory inside it, pulls down all the data for that repository, and checks out a working copy of the latest version. If you go into the new libgit2 directory, you�ll see the project files in there, ready to be worked on or used. If you want to clone the repository into a directory named something other than 'DemoProject', you can specify that as the next command-line option:
```PowerShell
git clone https://github.com/<username>/DemoProject MyDemoProject
```
That command does the same thing as the previous one, but the target directory is called MyDemoProject.

## Branches
 Branching means you diverge from the main line of development and continue to do work without messing with that main line.   
in other words: a branch is a parallel version of the main version or default branch
Use branches to  
* Develop features
* Fix bugs
* experiment with new ideas

Once satisfied with the result, you can merge the 'development' branch with the main code in the 'master' branch

### Creating branches
You�ve decided that you�re going to work on issue #53 in whatever issue-tracking system your company uses. To create a branch and switch to it at the same time, you can run the git checkout command with the -b switch:
```PowerShell
git checkout -b iss53
```
The previous command create a new branch iss53 and selected it as our working branch

This is shorthand for:
``` PowerShell
git branch iss53
git checkout iss53
```

if we want to browse to the main or master branch again, just type the following:
```PowerShell 
git checkout master
```
Did you notice that the file created in the iss53 branch just disapeared from our explorer?
So the cool thing is, each branch contains his working copy.

Once our issue or new feature has been tested and proved working, we do want to merge it with our main branch.

### Merging branches
Merging branches copies the changes from a branch to the working branch
So let's merge the iss53 changes with the master branch
``` PowerShell
git checkout master
git merge iss53
```

Now that all changes in branch iss53 have been copied to our nmaster branch we do not need the branch iss53 anymore and we can safely delete it
```PowerShell
Git branch -d iss53
```
# A word on the Git(hub) flow
 the github flow describes a way of working. It is actually very efficient.
 Basically you create a 'branch' for every 'change' you are making. Once the change proves to be  working, you merge it with the 'master' branch
 <INSET IMAGE HERE>
 GitHub Flow is a lightweight, branch-based workflow that supports teams and projects where deployments are made regularly. This guide explains how and why GitHub Flow works.
 more info can be found on https://guides.github.com/introduction/flow/index.html
 
# Collaborating
All previous examples showed the basics to start using git as your source control system.  
Github is know for adding a social layer on top of git and has been successful doing so. Collaborating and sharing is one of the key elements.
We do have our own public Organization with a public repository ready for collaboration or 'Forking'

## Forking a repository in Github
A fork is a copy of a repository. Forking a repository allows you to freely experiment with changes without affecting the original project.
Most commonly, forks are used to either propose changes to someone else's project or to use someone else's project as a starting point for your own idea.

A great example of using forks to propose changes is for bug fixes. Rather than logging an issue for a bug you've found, you can:
Fork the repository.
Make the fix.
Submit a pull request to the project owner.

If the project owner likes your work, they might pull your fix into the original repository!

On github, navigate to https://Github/Inovativ/DemoProject.
In the top-right corner of the page, click Fork.

You now have a copy of the original repository.
If you fork a project in order to propose changes to the upstream (original project) it is a good practice to regulary sync with the original repository.

Let's clone this to have a local working copy
```PowerShell
git clone https://Github/<username>/DemoProject
``` 

## Keeping in sync with the original repository

In order to keep in sync with the original repository we need to add the link.
Similar to adding a remote origin, we add an upstream.

to obtain the upstream url;
1. browse to the original project on github
2. on the right sidebar of the repository page, click the copy icon next to the clone url
3. open the git Shell and enter the following command 

```PowerShell
git remote add upstream https://github.com/Inovativ/DemoProject.git
```
and verify
```PowerShell
git remote -v
```
### Syncing a fork
Adding the upstream makes it possible to sync the with the original repository, but this still requires an intervention

```PowerShell
git fetch upstream
```
the commits of the original repository have now been captured to the upstream/nmaster branch
to merge them in our master branch we need to check it out
```PowerShell
git checkout master
```
and let's merge the changes
```PowerShell
git merge upstream/master
```

## Pull requests
Pull requests are an essential action when collaborating.
a pull request can be translated to: 'You send the author(s) of the original repository a request to help out'
Once the pull request has been accepted, it will be merged into the selected branch of the original repository.

### Creating pull requests
Create a pull request to propose and collaborate on changes to a repository. These changes are proposed in a branch, which ensures that the master branch is kept clean and tidy. 

Pull requests can only be opened if there are differences between your branch and the upstream branch. You can specify which branch you'd like to merge your changes into when you create your pull request.
1. On GitHub, navigate to the repository from which you'd like to propose changes..
2. Branch dropdown menuIn the "Branch" menu, choose the branch that contains your commits. .
3. Pull Request buttonTo the left of the "Branch" menu, click the green Compare and Review button. .
4. Edit button for compare pageThe Compare page will automatically select the base and compare branches; to change these, click Edit. .
5. Create pull request buttonOn the Compare page, click Create pull request. .
6. Pull Request description pageType a title and description for your pull request. .
7. Send Pull Request buttonClick Create pull request. .

After your pull request has been reviewed, it can be merged into the repository.


#Additional info
 * Git pro (book)[url] http://git-scm.com/book/en/v2
 * Github getting started
 * Powershell summit getting started with github
 * 