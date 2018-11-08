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
- [Deleting the feature Branch]()
- [Tracking the Uncommited/Untracked file]()
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

