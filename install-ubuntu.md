Installation
============

- necessary ubuntu apps

	```
sudo apt-get update
sudo apt-get install -y vim openssh-server htop tmux unrar git ipython default-jre default-jdk git-core zsh nginx python-pip python-setuptools python-dev
	```

SSH
===

- change default ssh port

	```
sudo vim /etc/ssh/sshd_config
sudo service ssh restart
ssh <username>@penguin.iis.sinica.edu.tw -p <port>
	```

motd (optional)
==============

- quickstart: download [this repo](https://github.com/maxis1718/update-motd.d)

- In Ubuntu Server 14.04, the motd are spread in several files under `/etc/update-motd.d`

	```
drwxr-xr-x   2 root root 4.0K Sep 18 17:03 .
drwxr-xr-x 106 root root 4.0K Sep 18 16:57 ..
-rwxr-xr-x   1 root root 1.2K Feb 19  2014 00-header
-rwxr-xr-x   1 root root  454 Sep 18 17:01 01-ascii-art
-rwxr-xr-x   1 root root 1.4K Feb 19  2014 10-help-text
-rwxr-xr-x   1 root root  149 Aug 22  2011 90-updates-available
-rwxr-xr-x   1 root root  299 Apr 11 15:06 91-release-upgrade
-rwxr-xr-x   1 root root  142 Aug 22  2011 98-fsck-at-reboot
-rwxr-xr-x   1 root root  144 Aug 22  2011 98-reboot-required
	```

- The system will assembly each part by the order of fileanmes.

- After making some changes, run `sudo run-parts /etc/update-motd.d/`.

- run `figlet penguin` to add a [`figlet`](http://patorjk.com/software/taag/#p=testall&f=Doh&t=penguin) like:
	
	```
	                               _       
	  _ __   ___ _ __   __ _ _   _(_)_ __  
	 | '_ \ / _ \ '_ \ / _` | | | | | '_ \ 
	 | |_) |  __/ | | | (_| | |_| | | | | |
	 | .__/ \___|_| |_|\__, |\__,_|_|_| |_|
	 |_|               |___/               
	```


Users & Groups
==============

#### 1. config `adduser` via editing `/etc/adduser.conf`

- use zsh as default shell

	```
DSHELL=/usr/bin/zsh	
	```

- /home/\<groupname>/\<username>

	```
GROUPHOMES=yes	
	```

- all users belong to the group __lwkulab__

	```
USERGROUPS=no
EXTRA_GROUPS="lwkulab"
ADD_EXTRA_GROUPS=1
	```

#### 2. config user template in `/etc/skel`

- edit template while a new user created

	```
sudo mkdir projects
cp -r /home/maxis/my-dotfiles .
cd my-dotfiles
sudo ./setup.sh
	```
	
- after creating basic directory and links, run `ls /etc/skel -ahl`, it looks like this

	```
drwxr-xr-x   4 root root 4.0K Sep 22 07:47 .
drwxr-xr-x 106 root root 4.0K Sep 22 07:45 ..
lrwxrwxrwx   1 root root   28 Sep 22 07:47 .bashrc -> my-dotfiles/dotfiles/.bashrc
lrwxrwxrwx   1 root root   31 Sep 22 07:47 .gitconfig -> my-dotfiles/dotfiles/.gitconfig
lrwxrwxrwx   1 root root   38 Sep 22 07:47 .gitignore_global -> my-dotfiles/dotfiles/.gitignore_global
drwxr-xr-x   7 root root 4.0K Sep 22 07:47 my-dotfiles
lrwxrwxrwx   1 root root   29 Sep 22 07:47 .profile -> my-dotfiles/dotfiles/.profile
drwxr-xr-x   2 root root 4.0K Sep 19 04:17 projects
lrwxrwxrwx   1 root root   30 Sep 22 07:47 .screenrc -> my-dotfiles/dotfiles/.screenrc
lrwxrwxrwx   1 root root   31 Sep 22 07:47 .tmux.conf -> my-dotfiles/dotfiles/.tmux.conf
lrwxrwxrwx   1 root root   27 Sep 22 07:47 .toprc -> my-dotfiles/dotfiles/.toprc
lrwxrwxrwx   1 root root   27 Sep 22 07:47 .vimrc -> my-dotfiles/dotfiles/.vimrc
lrwxrwxrwx   1 root root   27 Sep 22 07:47 .zshrc -> my-dotfiles/dotfiles/.zshrc
	```
	
#### 3. Groups

- add user group __lwkulab__
		
	```
sudo addgroup lwkulab
	```

- Finally, add a new user

	```
sudo adduser <username>
	```

---


HttpServer
==========

- install `nginx`

	```
sudo apt-get install -y nginx
	```

- check ip address

	```
ip addr show eth1 | grep inet | awk '{ print $2; }' | sed 's/\/.*$//'
	```	
	
- stop, start, restart

	```
sudo service nginx stop|start|restart
	```
- restart acutomatically

	```
sudo update-rc.d nginx defaults
	```

Database
========

- install `mongodb`

	```
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10
echo 'deb http://downloads-distro.mongodb.org/repo/ubuntu-upstart dist 10gen' | sudo tee /etc/apt/sources.list.d/mongodb.list
sudo apt-get update	
sudo apt-get install -y mongodb-org
	```

- start/stop/restart `mongodb`

	```
sudo service mongod start|stop|restart	
	```

- issues on a **NUMA** machine [(reference)](http://docs.mongodb.org/manual/administration/production-notes/)

	> Running MongoDB on a system with Non-Uniform Access Memory (NUMA) can cause a number of operational problems, including slow performance for periods of time or high system process usage.
	
	> When running MongoDB on NUMA hardware, you should disable NUMA for MongoDB and instead set an interleave memory policy.
	
	- disable NUMA for MongoDB and set an interleave memory policy
		
		```
sudo apt-get install numactl
numactl --interleave=all mongod
		```
	- disable zone reclaim in the proc settings
	
		```
echo 0 > /proc/sys/vm/zone_reclaim_mode
		```

	- setup `dbpath`

		```
dbpath (/data/db) does not exist.
Create this directory or give existing directory in --dbpath.
See http://dochub.mongodb.org/core/startingandstoppingmongo
		```


on-my-zsh
=========

- install

	`git clone --recursive git@github.com:maxis1718/maxis-dotfiles.git`

- reload tmux

	`:source-file ~/.tmux.conf`
	`tmux source-file ~/.tmux.conf`
	
curl -L http://install.ohmyz.sh | sh


Python
======

- useful python package

	```
sudo pip install -U flask pymongo beautifulsoup4 gunicorn Django nltk
	```

	- Database
		- SQLAlchemy
		- Pymongo
	- Scientific
		- numpy
		- SciPy
		- scikit-learn		
		
		```
		sudo pip install --user --install-option="--prefix=" -U scikit-learn
		```
     
	- Web Development
		- Flask
		- Django
		- [web.py](http://webpy.org/) `sudo easy_install web.py`
		- gunicorn
	- HTML/XML Parser
		- Beautiful Soup
		- PyQuery
		- lxml
	- NLP
		- nltk
	- Plotting
		- Matplotlib
		- ReportLab
