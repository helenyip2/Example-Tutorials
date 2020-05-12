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

SSH is a communication protocol standing for Secure Shell. It is a way that lets you do anything on a remote computer. The traffic travelling back and forth is encrypted. It is most oftenly used in terminal or command line.

When you're using SSH, you'll in an SSH client for you to remote into another computer. The computer you're trying to remote into needs to have a SSHD running on it. SSHD is an OpenSSH server that listens to incomming conenctions using SSH protocols and acts as server for the protcol.

On the SSH client, a ssh private and public key is created.
The private SSH key will be added to the ssh-agent on your local computer. The public key is added to SSHD server of where you want to SSH into.

## How to use it with Github?

##References
* https://help.github.com/en/github/using-git/which-remote-url-should-i-use
* https://help.github.com/en/github/authenticating-to-github/about-ssh
* https://help.github.com/en/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent

