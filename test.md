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
- [Setting up the remotes]()
- [Creating a feature branch]()
- [Taking Daily Update]()
- [Tracking the conflict file]()
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













