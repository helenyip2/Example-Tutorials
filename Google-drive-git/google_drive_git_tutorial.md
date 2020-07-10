# Using `git` on Google Drive

## Introduction

When you use Google Colaboratory notebooks in Google Drive the it autosaves autosaves every couple minutes. You can always go back to the last 100 autosaves of the notebook. This is probably around 3 hours of when you open up the notebook.

What if you did around 3 hours of work on it, and the notebook crashes or stops working? How to you get your notebook back to the state that you were at yesterday?

If you want to do this, you're better off turning your Google Drive folder into a local git repository.

**Why not just use the GitHub integration that Google Colaboratory notebook has?**

Google Drive is able to save a copy of your notebook to you GitHub repository, but it won't be able to commit other files along with it that might be needed for the file to work. (Such as a data file or commiting a pickle file as well.)

The only way you'd be able to commit both a copy of the notebook and another file in the folder together is to download it onto your computer, then push it. What a hassle.

In this tutorial, we are going to directly interact with git and GitHub through Google Drive.

## Goal

In order to follow along with the instructions, you'll need some basic git command line knowledge & how to use the terminal functions within a Colaboratory notebook.

In this tutorial, you are going to be doing the following:
* [Getting a Personal Access Token from GitHub](#getting-a-personal-access-token-from-github)
* [Cloning a GitHub repository](#cloning-github-repo)
* [Initializing a local git repository in Google Drive Folder](#intializing-a-local-git-repo-in-google-drive-folder)
* [Pushing local git repository from Google Drive to Remote Repository on GitHub](#pushing-local-git-repo-to-remote-repogithub)

Generally, Terminal or Command Line needs to be used when cloning GitHub repositories or making a local git repository. In this tutorial, we are going to be opening another Colaboratory notebook within your Google Drive to use as your terminal.

**Note**: Repository is going to be shorten to repo from now on.

## Getting a Personal Access Token from GitHub

When using Colaboratory notebook as the terminal, it won't prompt you for a password when you're interacting with with GitHub repos. Thus a personal access token is neccessary in proving that you have access to the repo through your account.

Follow the instructions from this [link](https://docs.github.com/assets/images/help/repository/https-url-clone.png) to get one.

Remember to treat this access token like you would treat any other password.

## Cloning GitHub Repo

As mention before in the previous section, the prompt to enter the password won't pop up when using Colaboratory Notebooks as the terminal to interact with GitHub. You won't need this if you you have access to clone the repo from GitHub, but you'll need use either the password or the personal access token when pushing commits to the Github repo.

We will be needed go use a personal access token that we got [above](#getting-a-personal-access-token-from-github) for this.

1. Open another colab notebook outside the folder in question. Name the notebook `terminal.ipynb`.

**Note:** I'd advising to keep the notebook outside the folder in question, so you don't accidently upload it with your personal access token in it. Another method is to start your notebook inside the folder in question and add `terminal.ipynb` to the `.gitignore` file.

2. You must mount Google Drive to any Colaboratory Notebook if you want to use it as your terminal in `terminal.ipynb`.

```python
from google.colab import drive
drive.mount('/content/drive')
```

This will prompt you to authorize to mount your Google Drive. Make sure you do that and enter in your authorization code from the website.

See [this](https://www.marktechpost.com/2019/06/07/how-to-connect-google-colab-with-google-drive/) for more details if you're interested.

3. In the Colaboratory notebook, unhide the menu on the left hand side. Find the folder where you want the new cloned repo to live in and copy the file path for it. Once you `cd` into this folder, you can clone the repo.

```bash
%cd [path_where_you_want_to_be_at]
```

4. Copy the HTTPS of the GitHub repo.

On the GitHub repository page look for a green button that says **Clone or download** on the right hand side of the page.

![Github repo https button](https://help.github.com/assets/images/help/repository/remotes-url.png)

It should be in the following format:

```
https://github.com/[User name]/[repository name].git
```

5. Edit the Github Repo's HTTPS to include the GitHub personal access token that you gotten [above](#getting-a-personal-access-token-from-github).

It should look like this:

```
https://[github-token]@github.com/[User name]/[repository name].git
```

6. Now clone run the command to clone the GitHub repo.

```
git clone https://[github-token]@github.com/[User name]/[repository name].git
```

You now have a cloned repo in your Google Drive!

---

>To double check that the the repo has cloned either:
>
> Run the following command in terminal to see if the GitHub repo name pop ups as a folder.
> 
> ```bash
> !ls
> ```
> 
> **OR**
> 
> Refesh your Google Drive page. Go into the folder that you `cd` into earlier. Check if the the GitHub repo is now listed in the folder.

## Intializing a Local Git Repo in Google Drive Folder

These are the steps to intializing a Google Drive folder into a git repo.

1. Open another colab notebook outside the folder in question. Name the notebook `terminal.ipynb`

2. Mount the the google drive into the notebook.
```python
from google.colab import drive
drive.mount('/content/drive')
```
This will prompt you to authorize to mount your Google Drive. Make sure you do that and enter in your authorization code from the website.

3. Open the left hidden menu within the Colaboratory notebook, open the file path, copy the file path for the folder in question.

In another cell, put in the following

```bash
%cd [paste in file path here. Put in quotes if there are spaces in it.]
```

Double check that you're in the right repository using `pwd`.

4. Now you're ready to initialize the google folder into the local git repository.

```bash
!git init
```

You can double check that it's been intialize by the following methods:

- Checking by using `!git status`

**OR**

- Go to your folder within your Google Drive, refresh the page & see if there's a `.git` folder in it.

5. Do everything else that you need to do in order to commit the file.

**Note:** You'll need to recreate your git config file everytime you restart the terminal.

```bash
!git config --global user.name [your username]
!git config --global user.email [your email address]
```

## Pushing Local Git Repo to Remote Repo(Github)

1. Create a new repo in your GitHub account.

2. Copy the HTTPS of your GitHub repo & add your GitHub personal access token into it.

```
https://[github-token]@github.com/[User name]/[repository name].git
```

3. Use the edited HTTPS to create a git remote for the github repo.

```bash
!git remote add [alias] https://[github-token]@github.com/[User name]/[repository name].git
```

Double check that the remote is added with the following.

```bash
!git remote -v
```

`-v` means to output more information regarding the remote.


5. Push your local repo into your github repo.

```bash
!git push -u [remote alias] [branch you want to push to on Github]
```

## Recap

In order to clone a Github repo into Google Drive or push a local git repo from Google Drive, you need the following:
* A Colaboratory notebook with the Google Drive mounted
* Personal access token from your GitHub account
* GitHub repo HTTPS

The GitHub repo needs to be refigured in the following format:
```
https://[github-token]@github.com/[User name]/[repository name].git
```

From there, you can either use it to `git clone` a Github repository or use `git remote` to link it to a Github repository.


## References

* [Link](https://zerowithdot.com/colab-github-workflow/)
* [Github Cloning Repo Tutorial](https://docs.github.com/en/github/creating-cloning-and-archiving-repositories/cloning-a-repository)
