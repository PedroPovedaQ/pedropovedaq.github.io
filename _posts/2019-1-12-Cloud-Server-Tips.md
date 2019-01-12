---
layout: post
title: Cloud Server Initial Setup Guide
---

So you just created a new droplet on Digital Ocean. Sweet. These are some preliminary steps you want to do to keep your droplet secure from yourself and shady characters on the internet.


### Make sure you have an ssh key.
To create a new key, type `ssh-keygen –t rsa` and follow the prompts.

### Create a new user with sudo permissions. Replace $USERNAME with your username of choice.
`$ adduser $USERNAME`
### Add the user to the sudo group so it has admin abilities.
`$ usermod –aG sudo $USERNAME`
### Switch to the user you just created and add your ssh public key.
``` $ su $USERNAME ```

Next, create a new directory called .ssh, set permissions, and add the authorized_keys.
``` $ mkdir ~/.ssh
$ chmod 700 ~/.ssh
$ vi ~/.ssh/authorized_keys
 ```
Paste your public key from your machine into the `authorized_keys` file and save.

### Disable logging in via password. 
Machines can guess passwords, especially simple ones. If the login process is ssh only it’ll be a lot harder to crack. While we’re configuring our ssh settings, let’s also disable logging in as root. We can still do everything we would want to do as sudo, but we’ll get at least a warning before we blow something up.
* Open your server's ssh configuration with ` $ sudo vi /etc/ssh/sshd_config`
* Change `Password Authentication yes` to ` Password Authentication no`
* Change `Permit Root Login yes` to ` Permit Root Login no`

### Restart SSH
Finally, restart SSH for these settings take effect.
`$ sudo service ssh restart`

### 👍
And there you have it, the bare minimum security requirements for a brand new cloud server. Now go take over the world.
