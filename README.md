# Using `git` on Google Drive

## Introduction

When you use Google Colaboratory in Google Drive the notebook autosaves autosaves every couple minutes. You can always go back to the last 100 autosaves of the notebook. This is probably around 3 hours of when you open up the notebook.

What if you did around 3 hours of work on it, and the notebook crashes or stops working? How to you get your notebook back to the state that you were at yesterday?

If you want to do this, you're better off turning your google drive folder into a local git repository.

How do we use git to keep track of our work that uses Google Drive?

**Why not just use the GitHub integration that Google Colaboratory notebook has?**

What if also a pickle file in the folder as well and you want to push that to GitHub? It's a lot of re-downloading on your computer in order to push it onto GitHub.

In order to follow along with the instructions, you'll need some basic git command line knowledge & how to use the terminal function within a Colaboratory notebook.

## Goal

In this tutorial, you are going to be doing the following:
* Getting a Personal Access Token from GitHub
* Cloning a public GitHub repository.
* Cloning a private GitHub repository.
* Initializing a local git repository in GitHub.
* Pushing local git repository from Google Drive to GitHub.

Generally, Terminal or Command Line needs to be used when cloning Github repositories or making a local git repository. In this tutorial, we are going to be opening another Colaboratory notebook within your drive to utilize as your terminal.

**Note**: repository is going to be shorten to repo from now on.

## Getting a Personal Access Token from GitHub

The first thing is to get a personal access token from Github. Follow the instructions from this [link](https://help.github.com/en/github/authenticating-to-github/creating-a-personal-access-token-for-the-command-line) to get one.

Remember to treat this access token like you would treat any password.

Colaboratory notebook's terminal won't prompt for a password when interacting with GitHub repos. Thus a personal access token is neccessary.

## Cloning a Public GitHub Repo

1. You must mount Google Drive to any Colaboratory Notebook if you want to use it as your terminal.

```python
from google.colab import drive
drive.mount('/content/drive')
```

This will prompt you to authorize to mount your google drive. Make sure you do that and enter in your authorization code from the website.

See [this](https://www.marktechpost.com/2019/06/07/how-to-connect-google-colab-with-google-drive/) for more details if you're interested.

2. If you want to just clone any Public GitHub Repo, just copy the HTTPS of the repo.

3. In the left hand menu, find the folder where you want the new cloned repo to live in and copy the file path for it. Once you `cd` into this folder, you can clone the repo.

```bash
%cd [path_where_you_want_to_be_at]
!git clone [github_repo_HTTPS]
```

You now have a cloned repo in your Google Drive!

Note: If you want to push commits to this repo, you will need to clone it the way you do private GitHub repos as you need your password. See the section below.

## Cloning Private GitHub Repos

When trying to clone a private repo, the terminal will prompt for an username and password. In Colaboratory notebook, the prompt to enter the password won't pop up.

We will be needed go use a personal access token that we got above for this.

Usually when you're trying to clone a repo, you're able to get the HTTPS for the repository in the following format:

```
https://github.com/[User name]/[repository name].git
```

Since the `git clone` function will not prompt for the username and password, the personal access token will need to be inserted into the HTTPS of the github repo.

```
https://[github-token]@github.com/[User name]/[repository name].git
```

Thus the `git clone` command will look like this:

```
git clone https://[github-token]@github.com/[User name]/[repository name].git
```

## Intializing a Local Git Repo in Google Drive Folder

These are the steps to intializing a Google Drive folder into a git repo.

1. Open another colab notebook outside the folder in question. Name the notebook `terminal.ipynb`

2. Mount the the google drive into the notebook.
```
from google.colab import drive
drive.mount('/content/drive')
```
This will prompt you to authorize to mount your google drive. Make sure you do that and enter in your authorization code from the website.

3. Open the left hidden menu within the Colaboratory notebook, open the file path, copy the file path for the folder in question.

In another cell, put in the following

```
%cd [paste in file path here. Put in quotes if there are spaces in it.]
```

Double check that you're in the right repository using `pwd`.

4. Now you're ready to initialize the google folder into the local git repository.

```
!git init
```

You can double check that it's been intialize by the following methods:

- Checking by using `!git status`

**OR**

- Go to your folder within your Google Drive, refresh the page & see if there's a `.git` file in it.

5. Do everything else that you need to do in order to commit the file.

## Pushing Local Git Repo to Remote Repo(Github)

1. Create a new repo within GitHub account.

2. Copy the HTTPS of your GitHub repo & add your GitHub personal access token into it.

```
https://[github-token]@github.com/[User name]/[repository name].git
```

3. Use the edited HTTPS to create a git remote for the github repo.

```
!git remote add [alias] https://[github-token]@github.com/[User name]/[repository name].git
```

Double check that the remote is added with the following.

```
!git remote -v
```

`-v` means to output more information regarding the remote.

4. Push your local repo into your github repo.

```
!git push -u [remote alias] [master]
```

## References

https://drive.google.com/drive/u/2/folders/1FxMy480WyeI0T3p-dTtI7Nz-VbcN2ulC folder where all this is in.
