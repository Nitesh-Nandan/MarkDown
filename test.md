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

As we have discussed eclipse plugin of git is very efficient when there are multiple repositories to work on. We will try to minimize our time and manual effort. This thing can be done through the bash script. We will use GIT bash as an environment to run the script.

Please [click here](/InstallationofGitBash.md) to see the installation process of Git Bash shell in system.

Let me give you a brief context of Git Bash Shell befory we continue. 