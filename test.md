# **HighRadius Git**
Git is a distributed version-control system used for source-code mangement. Unlike CVS it supports for non-linear development i.e. we can work on thousand of parrellel features at a time.

 In HighRadius we use Git through eclipse but the fact is git-plugin of eclipse is unable to utilize most of  the powerful featuere  of GIT.

I have written few shell scripts which makes our day today task very easy.

---

## **Challenges in Eclipse**

### WorkSpace Setup
This is one time setup and  might not be a big issue for a developer but definetly it is a boring to clone each repository one by one and setting up the remotes.
If we properly setup the remotes then this setup might take 60 minutes. My question is can we do something better? 

The above task can we done within 2 minutes with zero manual effort with the help of scripts.

### Daily Update
In HighRadius a product like EIPP has appx 10 repositories and to sync a branch in  our Local repostitory and User's Public Repositories with Official Reopositories we have to perform these three operation:

1. Fetch the latest changes from Official Repositories.
2. Merge the changes.
3. Push the changes to User's Public Reopositories.

This task has to be perfomed frequently as we have to work on latest code and if a repository has three branch ( generally we have ), we have repeat the same operation three times. This is time consuming and a very boring task for a developer like me.


### Working on Feature Branch

It is always better to work on a feature branch, in HighRadius feature branch is nothing but user story specific branch.

To work in user-story branch we have to first create a user-story branch in all the repositories, this is really once again a tidious task as we have to repeat the process for all the repositories. 

### Writing a Commit Message

Most of you might not be agree but believe writing a good commit message is not so easy, it takes times and there is high probablity that every time you chage your message format of commmit.

At later bad commit message become very difficult to track.

### Tracking the changes in User-Story Branch

In eclipse there is no way to track the files which are changed during the development of User-Story Branch. 

You can only compare your changes to some specific branch.

---

# Automate the Boring Stuff

As we have discussed eclipse plugin of git is very inefficient when there are multiple repositories to work on. We will try to minimize our time and manual effort. This thing can be done through the bash script. We will use GIT bash as an environment to run the script.

Please [click here](https://github.com/Nitesh-Nandan/MarkDown/blob/master/InstallationofGitBash.md) to see the installation process of Git Bash shell in system.

Let me give you a brief context of Git Bash Shell befory we continue. 

Bash is a UNIX Shell and command language interpreter, and git bash is build on top of it to support the git commands.



## Important Links
- [Boosting Git Bash Shell (Script Setup)]()
- [First time git setup]()
- [Setting up workspace]()
- [Setting up the remotes: See the Advantage]()
- [Creating a feature branch]()
- [Taking Daily Update]()
- [Checking the update status]()
- [Merging the feature Branch]()
- [Tracking the conflict file]()
- [Tracking the Uncommited/Untracked file]()
- [Deleting the feature Branch]()
- [Fetching the code from other user's cloud repository]()
- [Automatically Generating the commit message]()
- [Short Hand commands]()
- [Frequently asked questition (FAQ)]()


## **Boosting Git Bash Shell**

Once you have downloaded the git bash shell if not then please ([click here]()) to know the download procedure.

After successfull install:&nbsp; Steps to be followed:
- Step 1:&nbsp; Download or clone the Github Repostitory from [here](). <br> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url:&nbsp; www.gitNiteshNandan.com <br>

- Step 2:&nbsp; Copy the scripts folder and paste in your home directory. <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; for eg:&nbsp; C:/Users/nitesh.nandan (for me). <br>

- Step 3:&nbsp; Open the .bash_profile with text editor and replace nitesh.nandan to you ldap id. <br>

- Step 4:&nbsp; Save the file and paste in your home directory.<br>

- Step 5:&nbsp; If you already have .bash_profile then replace the file with this file.<br>

- ******************* DONE  **********************

## **First time git setup**

### Setting up email & username
<pre>
   $ git config --global user.name "nitesh.nandan"
   $ git config --global user.email "nitesh.nandan@highradius.com"
</pre>

Rememeber this username or email is not you credentials, actually there is no relation between your credentials and the username that you provided.

### Setting up your editor

Default Git Bash comes with vim editor (a unix command line editor). The editor is not very user friendly. So we will setup sublime text editor: a light weight cross-platform code editor.

You can download the portable version of editor from: <br>
&nbsp;&nbsp;&nbsp;&nbsp; Url:&nbsp; https://www.sublimetext.com/3 <br>
or you can [click here](https://www.sublimetext.com/3).

Once you downloaded the portable version, unzip the file. Open the folder 
you will se something like this: <br>

![](image/git-installation/step6.png)<br>

### Linking sublime text 3 to bash shell

Reaname the parent folder containing subl application as sublime and copy this folder to your C drive. (you have freedom to choose your suitable directory).

If you go with the C drive, the path of subl application should be "c:/sublime/subl.exe'. Open the command prompt and type full path of subl.exe, a sublime editor will be open confirming the correct path. Now link the same path to git bash, to do so open the git bash shell
<pre>
&nbsp;&nbsp; git config --global core.editor "'c:/sublime/subl.exe' -w"
</pre>

The linking of editor is finished.

### Making you file system platform independent

As we know, the code continously swithches between different platforms (linux, windows), the end of file is flag is different for both the platforms, so to maintain a uniformity across the platform we have to set clrf flag to false. Open your git bash: &nbsp;
<pre>
    git config --global core.autoclrf false
</pre>


## **Setting up workspace** 

In CVS we used to checkout the project, in similar way we clone the project in GIT. 

Every user has it's own public repository where the forked repository resides, and we clone from our public repository.
See the diagram: <br>

![](image/git-installation/step6.png)<br>

Most of the team in HighRadius works on multiple project, so cloning each project one by one using eclipse is not encouraged. 

So, there is a shell script (clone.sh) which clone all the project in one go. Here comes few modification in clone.sh script as per the team.

Open the clone.sh script in one of the text editor (you can use sublime is you have installed). You will find something like this: <br>


![](image/git-installation/step6.png)<br>


Here you have to change few line. At second line there will be eipp_cloud
variable which holds the projects name seperated by space. Change this varialbe according to your requirement.

The next variable is ldapIds for your team member. Repalce these ldapd's with you team member ldap's. In the next section I will be discuss the importance of ldap's.

There is two different ways in which you can run clone.sh.

<pre>
    $ clone [ldapId (username)]
    $ clone [ldapId (username)] [branch_name]
</pre>

Here ldapId is mandatory argument where branch_name is optional. 99.99% of the time we will not pass the branch_name since default it will checkout falcondev branch for you.

[-----Image for clone.sh------]()




#### Adding Cloned Repositories to the eclipse Workspace

- Step 1:&nbsp; Open Your eclipse and create a workspace. <br>
- Step 2:&nbsp; Go to Window > Show View, and search for Git Repositories and open it. <br>
- Step 3:&nbsp; click on <strong> Add an existing local Git Repository.</strong>. <br>

image is required

- Step 4:&nbsp; Browse to your local repository wher you have cloned the project. <br>

- image is required

Step5: Import these Project one by one, it will be added to project explorer.

-- image is required

Don't change any default setting click on finish button. Repeat the same for each project.

You can see the falcondev is checkout as your working branch in project explorer.

## **Setting up the remotes: See the Advantage**

You don't have to setup the remotes explictily, it has been taken care of while cloning the project itself. You might confused what are the remotes? 

Remotes are nothing but a reference or url of the repositories. Since Git is distributed system, we can have multiple cloned repository hence a multiple references. Let a example to understand better, A team has 15 developer, since all the developer works on their forked repository and forked repository is nothing but a clone of Official Repository. It mean we have 15 (user's public repository) + 1 (Official Repository), hence 16 different remotes of a repository.

#### Advantage

Now suppose you want to take some code that is in developing stage from few team members. In case of CVS we have no option other then explictily asking the code and sending throuhg the mail, but in GIT you can fetch the changes with the help of url, even you can compare you code and take only changes that you want, it is nothing but you can collabrate much easily with you team.

## **Creating a feature branch**

As per the simplicity you shouldn't on falcondev branch rather you should create a feature branch (user story) and work it. There are several advantage of doing so, I will discuss all these in coming sections. I assume you must be knowing how to create a branch in eclipse. Suppose in eclipse workspace we have 10 branch then to make a featute branch we have to go through each one of the repository, which is not very handy.

There is create_branch script which creates a feature branch in all the repositories in one go. 

Before you use the create_branch you should change few lines in the create_branch as per your team.


----- image

You can see similar to clone script there is eipp_cloud variable, modify the variable as you have done in clone script. Now you are ready to go.

<pre>
    $ create_branch [csw/sw] [branch_name]
</pre>

create_branch takes two argument first one is a flag and second one is branch_name.

 1. &nbsp; csw:&nbsp; It will create a new_branch and checkout the newly created branch.<br>
 2. &nbsp; csw:&nbsp; It will switch to branch existing one. (It will not create a new branch.)

 --- image to demomstrate the branch


## **Taking Daily Update (Syncing the Repositories) **

In HighRadius Git Workflow we have three repositories: <br>
1. &nbsp;<strong> Official Repository:</strong> &nbsp; This is the repository from where user forked. All the builds happen here and finally everyone contribute their changes here.<br>
2. &nbsp; <strong>User's Public Repository:</strong> &nbsp; This is forked repository from where we clone to our local. <br>
3. &nbsp; <strong>Local Repository:</strong> This repository resides in your local system (eclipse).

#### Convention over configuration

1. &nbsp; You should never work on falcondev, always create a feature-branch and work. <br>
2. &nbsp; Before running the script you should't have any untracked or modified file in your workspace (not mandatory but highly recommended). <br>
3. &nbsp; Commit your changes to your feature branch before running the daily_update script. <br>

#### Why these conventions: Behind the scene

The above conventions has made to keep our falcondev branch unchanged from your local change, hence the commit history will be remain unchanged and we can take the advantage of fast-forward merge which is conflict free merge.

There are basically two types of merge happens in GIT:
1. &nbsp; Fast-Forward Merge
2. &nbsp; Recursive Merge (three-way merge)

The detailed explanation is out of scope, for now we can say Fast-Forward merge is conflict free merge and it happens when commit history remains unchanged.

Daily Update script mainly do three operation for each of the branch:
1. &nbsp; It will fetch (download) all the upcoming changes from Official repository.
2. &nbsp; It will merge the latest fetched changes to your local repository branch.
3. &nbsp; Push the changes to your's cloud repository.

<strong>Note: &nbsp;</strong> Fetching (downloading) the changes never creates a conflict nor it changes you working directory, it updates only local remote directory.

<pre>
    $ daily_update [branch-name]
</pre>

Here branch-name is optional, if you don't provide the branch-name, after update you working branch will checkout.

## **Checking the update status**

The aim of daily_update script is to keep our local and forked repository w sync with the Official Repository. If the last commit id same in all the three repository, then we can say our repository are in sync, or commit in local falcondev should not be behind from the commit of Official Repository.

There is a script named as show_sync which helps you to decide whether your repositories are in sync or not. 

<pre>
    $ show_sync [repository-name]
</pre>

Here repository-name is optional argument, if you don't give it will show for all the repository that are listed in the script.

---image


## **Merging the feature Branch**

As we have discussed prviously, we should always work on feature branch, so when we done with our work, we should merge feature branch with the latest code of falcondev and push to our public repository.

Now the questiton is how effectively and efficiently we do the merge. There are several method through which we can merge the change, it totaly depend on the context.

These are the several methods: <br>
1. Recursive merge (Normal merge, three-way merge).<br>
2. Squash Merge <br>
3. Selective Merge.
4. Rebase 


<strong> Recursive Merge: &nbsp; </strong> This merge should be perfomed when the feature-branch has lots of changes and most of the file are new and probablity of getting conflicts is very less.

There is seperate script to perfom this kind of merge named as feature_merge.
This feature_merge will generate a  consolidated file of all the action also pointing out the conflict file if merge get failed. As per my experience in HighRadius, we perform these merge but not through the script because  our changes are limited to few repositories only.

The git command for this merge is: <br>
<pre>
    $ git merge [feature_branch]
</pre>

<strong>Notes: &nbsp;</strong> You should be carefull with your branch while merging, i.e. you should first checkout the branch where you want to merge your feature branch. 

for eg: &nbsp; Suppose you want to merge your feature_branch to falcondev, then before performing the action you should checkout falcondev and the run the command.


<strong> Squash Merge: &nbsp; </strong> The command for this merge is similar to the three-way merge, but the difference is it puts all your changes in a working/indexed area and from there you have to commit, this helps you to maintain a clean and tidy commit history.

The git command for this merge is: <br>
<pre>
    $ git merge [feature_branch] --squash
</pre>

<strong> Selective Merge: &nbsp; </strong> This merge is highly encouraged when there are high chance of getting the conflict or you have lots of small changes in a single file. This merge comes very handy while fixing the bug or doing the small changes. You will be doing this very often.

You can do selective merge through eclipse comparing the file with the feature branch file.

<strong> Rebase: &nbsp; </strong> I personally don't like this merge with the context of HighRadius. 

These are few reason why I don't like and also suggest not use:<br>
1. It merge your feature branch, with all the commits, which might be not necessay.
2. It will destroy the commit id and your feature branch.
3. It is little complex as compare to previously discussed merge.

## **Tracking the conflict file**

While merging the our changes, we often get the conflict, though eclipse will show the red mark after removing the conflict also it generally doesn't change. So, I have written a script to list down all the conflict files from your workspace, so once you do with the resolving with conflicts, you can run the script to cross check.

When there is conflict we get some conflict marker like:
<pre>
    <<<<<<< HEAD
        Hello world
        =======
        Goodbye
    >>>>>>> 
</pre>

So, the script search for the string "<<<<<<<" in your workspace, if it find it will reurn the absolute path of the file.

So, this script doesn't tell exactly whether the file has actual conflict or not. So if some developer used this symbol intentionally then also it will show as conflicted file, use you wisdom there. Generally we never use this symbol during development.

This script comes very handy when multiple file has conflict and you totaly lost the track.

## **Tracking the Modified/Untracked file**

As we work on multiple project and therefore somtimes it is become difficult to track all the changes what we made.

There is script called show_unt it will list down all the modified and untracked file from your workspace.

It comes very useful before running the daily_update as I have already suggested you should commit all your changes before taking daily_update.

The command goes like: <br>
<pre>
    $ show_unt
</pre>


## **Deleting the feature Branch**

As we usually worked on feature_branch, so when you done with the your task you might want to delete the branch. Therefore there is a script called 
delete_branch which does the same in all the repository of workspace.

There is two types of delete when comes to deleting the branch in git.
1. Soft delete
2. Hard delete

In soft delete the branch will not get deleted if it is not merged with any other branch. It will save you if you run the command by mistake.

In hard delete the branch will be deleted irrespective of whether it is merged or not. So, be carefull while perfoming the delete. 

Deleting the branch will also delete all the commit related to that branch.

script command: <br>
<pre>
    $ delete_branch [branch_name] [hard]
</pre>

Here branch_name is mandatory and hard is optional argument. If you don't provide hard, it will try to perform soft delete, or it will go for hard delete.

The git command for deleting the branch is: <br>
<pre>
    $ git branch -d [branch_name]                   // soft delete
    $ git branch -D [branch_name]                   // hard delete
</pre>


## **Fetching the code from other user's cloud repository**

I personally feel the power of distributed version system like GIT when collabration comes in picture. In CVS, we share our code throgh mail or drive, thanks to distributed system which makes very easy to share your code or even your workspace.

In clone script, I have introduced the concept of remote and while cloning a repository itself script will add all the remotes, so you don't need to add manually. 

#### Problem Statement: 
Let's suppose you and some of your team members are working on a user-story. During the development you want code from your group member, since code is not fully functional so your friend can't push the code to official repository. So how to take the Update?

Here comes remote in action, remote is nothing but a link to repository that also exist somewhere in the cloud. So as you are fetching the latest change from Official Repository, similar way you can also fetch the changes from your friends repository.

<strong> Note:&nbsp; </strong> In HighRadius everybody has read (fetch) aceess for all the repository exist in HighRadius git cloud.

Command for the Opearation:
<pre>
    $ git fetch [remote-name]
</pre>

Here remote-name is mandatory parameter which holds the link and references of the repository.

<strong> Note:&nbsp; </strong> This will only download the code from the link it will not merge to your working directory. So to take the change to working directory it has to be merged.

## **Automatically Generating the commit message**

The good commit message is always encouraged. You might fell writing a commit message is very easy, but believe me writing a good and clean commit message might not be so hard but it is time consuming. The another problem is suppose we write 10 commit message, there might be a high chance that we landup in 10 different format of commit message.

This only works when your commit the change using git bash.
After adding your changes in staging are you can commit as :
<pre>
    $ commit // this is modified version of git commit
    $ git commit // this is default command that git bash support
</pre>


This will open a editor (default editor) like this:

-- image


## **Short Hand commands**

These commands are written with the help of basic commands that exist in UNIX bash shell to save your time.

These short hand commands are called alias.<br>
<strong>Note: &nbsp;</strong> All short hand commands are present in <i>.bash_profile</i> file. You can chage the value as per your need.

### Basic Commands

1. <strong> &nbsp;subl: &nbsp;</strong> This comand will open your sublime text editor, if it is avialble in <i>C</i> drive. You can change the default location in <i>.bash_profile</i> file. <br>

2. <strong> &nbsp;repo: &nbsp;</strong> This command directly take you to the local repository where git repository is located.<br>

3. <strong> &nbsp;gd: &nbsp;</strong> This command directly take you to the desktop.<br>

4. <strong> &nbsp;ccd: &nbsp;</strong> This command takes one argument. This command will create a folder with the name passed as argument and also take you inside the newly created directory. This command is integration of two basic comands. <pre>
    $ mkdir [folder-name]
    $ cd [folder-name]
</pre>

5. <strong> &nbsp;del : &nbsp;</strong> It will take one argument and delete the file/directory as passed in argument.<br>

### Git Specific Commands


1. <strong> &nbsp;clone: &nbsp;</strong> It will take your ldapId (username) as argument and download all the forked repository listed in the script in current working directory. [Click Here]() for more details.<br>

2. <strong> &nbsp;graph: &nbsp;</strong> This command will display commit history graph of working git directory. [Click Here]() for more details.<br>


3. <strong> &nbsp;daily_update: &nbsp;</strong> This command will help you to keep your local and forked repository with Official Repository. [Click Here]() for more details.<br>

4. <strong> &nbsp;create_branch: &nbsp;</strong> This will create/switch to a feature branch or both. [Click Here]() for more details.<br>

5. <strong> &nbsp;delete_branch: &nbsp;</strong> This will delete the branch with name that has passed as argument. [Click Here]() for more details.<br><br>


6. <strong> &nbsp;feature_merge: &nbsp;</strong> It takes feature-branch name as argument and this branch will be merged to falcondev. Also generate a summary file named as <i>[feature-branch name]_merge_summary.txt </i>Click Here]() for more details. [Click Here]() for more details.<br>

7. <strong> &nbsp;show_sync: &nbsp;</strong> This script will help you to figure out whether you local and forked repository are on sync or not. [Click Here]() for more details.<br>

8. <strong> &nbsp;show_unt: &nbsp;</strong> This will display the list of all the modified or untracked file that has yet to commit. [Click Here]() for more details.<br>

9. <strong> &nbsp;show_pdiff: &nbsp;</strong> This will list down all the file name that has been created or modified in feature_branch.
<strong>Note: &nbsp;</strong> This command should only run in feature branch, created using create_branch script.<br>

10. <strong> &nbsp;show_diff: &nbsp;</strong> This will list down all the file name that has been created or modified from last commit. [Click Here]() for more details.<br>

11. <strong> &nbsp;show_cmg: &nbsp;</strong> This will display last generatd commit message.<br>

12. <strong> &nbsp;show_gcmg: &nbsp;</strong> This will generate a fresh commit message and diplay in bash shell. This should call when you are working on feature branch only.

13. <strong> &nbsp;git_help: &nbsp;</strong> This will be list down all the git specific customised commands.<br>
<strong>Note: &nbsp;</strong> you can also type alias in bash shell. It will print all alias (short-hand) commands present in <i>.bash_profile.</i><br>

14. <strong> &nbsp;last_commit: &nbsp;</strong> 

### Bonus Commands

1. <strong> &nbsp;node1: &nbsp;</strong> This will open the chrome browser<br>

2. <strong> &nbsp;node2: &nbsp;</strong> You can see FIT Node1 log using this command. Make sure you have the fit log access.<br>

2. <strong> &nbsp;node3: &nbsp;</strong> You can see FIT Node2 log using this command. Make sure you have the fit log access.<br>

2. <strong> &nbsp;chrome: &nbsp;</strong> You can see FIT Node3 log using this command. Make sure you have the fit log access.<br>

## **Frequently asked questition (FAQ)**

<strong> &nbsp;Q 1: &nbsp;</strong> How many local git repository we can have ? <br>
<strong> &nbsp;Ans: &nbsp;</strong> You can have as many as repositoy you want, until your's disk is run out of memory.<br> <br>

<strong> &nbsp;Q 2: &nbsp;</strong> How many feature branch I can create in git? <br>
<strong> &nbsp;Ans: &nbsp;</strong> You can create as many as branch, there is no limitation in no of branch.<br> <br>

<strong> &nbsp;Q 3: &nbsp;</strong>Is it mandatory to take daily update ? <br>
<strong> &nbsp;Ans: &nbsp;</strong> No, It is not mandatory to take the update daily but make sure befor you push your changes it should have updated code and doesn't break functionality.<br> <br>

<strong> &nbsp;Q 4: &nbsp;</strong> How many feature branch I can create in git? <br>
<strong> &nbsp;Ans: &nbsp;</strong> You can create as many as branch, there is no limitation in no of branch.<br> <br>

<strong> &nbsp;Q 5: &nbsp;</strong> How many feature branch I can create in git? <br>
<strong> &nbsp;Ans: &nbsp;</strong> You can create as many as branch, there is no limitation in no of branch.<br> <br>

<strong> &nbsp;Q 6: &nbsp;</strong> How many feature branch I can create in git? <br>
<strong> &nbsp;Ans: &nbsp;</strong> You can create as many as branch, there is no limitation in no of branch.<br> <br>

<strong> &nbsp;Q 7: &nbsp;</strong> How many feature branch I can create in git? <br>
<strong> &nbsp;Ans: &nbsp;</strong> You can create as many as branch, there is no limitation in no of branch.<br> <br>



