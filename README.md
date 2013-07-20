Minecraft Multi-Server Initializer
=======================================
A minecraft server initialize script that allows you to manage multiple servers.

Features
--------

 * Create, Delete, Rename, Copy Minecraft Servers
 * Allows creation off servers with different ram allocations, cpu coress and jar files.
 * Backups off worlds and complete servers into a different location to the servers.
 * Server updating for vanilla and craftbukkit servers
 * Exclude files and directories from full backup by adding them to "exclude.list"
 * WorldEdit compatible backups
 * Loading off worlds into system RAM for faster access (redcing lag)
 * Allows sending off commands to servers via command line
 * Uses screens for console access (info below)

Dependencies
------------
screen, rsync, java

Getting Started
===============

Installing Dependencies
-----------------------

Installing screen & rsync

On Red Hat-based distributions:

  		yum install screen
		yum install rsync
	
On Debian based systems such as Ubuntu:

		apt-get install screen
		apt-get install rsync
	
Installing Java 7

On Red Hat-based distributions:

		yum install java

On Debian based systems such as Ubuntu:

		apt-get install openjdk-7-jre
		apt-get install openjdk-7-jdk
		update-alternatives --config java


Enabling MCInitializer
----------------------

1. Symlink the minecraft script to `/etc/init.d/minecraft`

		sudo ln -s ~/mcinitializer/minecraft /etc/init.d/minecraft
   
   Set the correct permissions on the minecraft script
   
		chmod 755  ~/mcinitializer/minecraft
   
   Finally, update rc.d to start the servers when the system starts
   
		sudo update-rc.d minecraft defaults

2. Edit the variables in `config.example` once done, rename it to `config`

3. Edit crontab

	As the server user you're running the script as:
	
		crontab -e

	Add these lines:

		#m 	h 	dom	mon	dow	command
		54 0,11 * * * /etc/init.d/minecraft say 'Server restart in 5 minutes!'
		58 0,11 * * * /etc/init.d/minecraft say 'Server restart in 1 minute!'
		59 0,11 * * * /etc/init.d/minecraft restart
		02 05  *   *   *   /etc/init.d/minecraft backup
		55 04  *   *   *   /etc/init.d/minecraft log-roll
		*/30   *   *   *   *   /etc/init.d/minecraft to-disk
	
Commands
===============

To view all commands do

	/etc/init.d/minecraft help
	
To view all server commands do

	/etc/init.d/minecraft SERVER_NAME help
	
Console Access
===============

  screen -r SERVER_NAME

Or

  /etc/init.d/minecraft SERVER_NAME screen

To exit console:
	
	Ctrl+A D

