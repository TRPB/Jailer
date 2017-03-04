# Jailer

A tool for quickly creating SSH Chroot Jails.


## Installation

*Jailer requires PHP 5.6 or higher.*

Run the following with root privileges:

```
wget -O /usr/bin/jailer https://github.com/TomBZombie/Jailer/blob/master/jailer
chmod +x /usr/bin/jailer

```


## Usage

To use jailer, create the directory that will serve as the chroot jail then navigate to it and run `jailer init`:

```
cd /path/to/jail
jailer init
```

Create a user with useradd and add the user to the jail:

```
useradd [name]
passwd [name]
jailer user [name]
```

*You can add as many users to the jail as you like*

And now allow the jailed users to access any programs:

```
# allow the jailed user to run git
jailer allow git

# allow the jailed user to run php
jailer allow php
```


By default, jailed users do not have access to any programs at all including `ls`, `cp`, etc. To give the user access to `ls`, `cp`, `mv` and `rm` run the command:

```
jailer allow fstools
```


## Jailing the user on SSH

The tool does not amend your `sshd_config` automatically as the location can vary on systems. On most systems this is stored in `/etc/ssh/sshd_config`. Once you have created the jail you will need to amend the file with the following:

```
Match User [name]
	ChrootDirectory /path/to/jail
```

*The tab before `ChrootDirectory` is required.
