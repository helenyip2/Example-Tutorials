# How to use SSH with Github

When you're trying to clone a GitHub repository into your you see that there's 2 different options when you click on the on the green Clone or download button.

1. Clone with HTTPS

![github_http_image](github_http_image.png)

These are available on all public and private Github reposoitories. This is probably what you've used before when you've clone a repository from Github.

When you use this method, the remote that's saved in your local git repository will be in the following format. I'm using this current Github repository as an example.
```
https://github.com/helenyip2/Example-Tutorials.git
```

Every time you use the commands listed below in command line, you'll be prompted to enter in your Github username and your password.
* `git clone`
* `git fetch`
* `git pull`
* `git push`

2. Clone with SSH

![github_http_image](github_ssh_image.png)

When you're using the SSH URL you'll be GitHub via SSH. In order to do this, you'll need to have a SSH key registered with your GitHub account. We will go into this later.

When you use this method, the Git remote that's saved in your local git repository will be in the following format. I'm using this currently Github repository as an example.
```
git@github.com:helenyip2/Example-Tutorials.git
```

When you access GitHub via SSH, you'll not be prompted to enter your GitHub username and password every time you use the following commands:
* `git clone`
* `git fetch`
* `git pull`
* `git push`

This is because GitHub already knows that who you are because of the SSH key registered with the account.

## What is SSH?

## How to use it with Github?

##References
* https://help.github.com/en/github/using-git/which-remote-url-should-i-use
* 

