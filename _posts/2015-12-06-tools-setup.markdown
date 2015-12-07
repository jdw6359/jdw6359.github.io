---
layout:     post
title:      "Application Prerequisites"
subtitle:   "How to get up and running with the Particip8 application."
date:       2015-12-06 12:00:00
author:     "Josh Woodward"
header-img: "img/boba.jpg"
---

<p>This series of posts will assist you in getting the Particip8 application up and running. In this post, I will walk you through the installation of several application prerequisites on the AWS EC2 Ubuntu Server. The topics discussed here include Git, Redis, and RVM. A future post will discuss the work necessary to host the application.</p>    

<h2 class="section-heading">Prerequisites</h2>
<p>Prior to installing anything on our Ubuntu server, we must first make sure that we have installed, configured, and accessed our EC2 instance. The steps necessary to setup the server can be found here: <a href="https://jdw6359.github.io/2015/12/06/EC2-setup/">Ubuntu EC2 Setup</a></p> 

<h2 class="section-heading">Installing Git</h2>
<p>The deployment of our project source onto the server relies on Git, so this must be installed. Simply install the Git package as follows:</p>
<blockquote>
$ sudo apt-get install git
</blockquote>

<h2 class="section-heading">Installing Redis</h2>
<p>Our system stores a portion of its data in Redis, a simple key-value store. You may read more about Redis here: <a href="http://redis.io/">Redis Information</a></p>

<p>We will now install, build, and start the Redis server</p> 

<p>First, let's make sure that our system has the packages necessary to build Redis:</p>
<blockquote>
$ sudo apt-get install build-essential<br>
$ sudo apt-get install tcl8.5
</blockquote>

<p>The Redis source tarball can then be grabbed from the Redis download server :</p>
<blockquote>
$ wget http://download.redis.io/releases/redis-stable.tar.gz
</blockquote>

<p>Let's unpack the .tar, and then get rid of it!</p>
<blockquote>
$ tar xzf redis-stable.tar.gz<br>
$ rm redis-stable.tar.gz
</blockquote>

<p>We will now build Redis from source, and run the provided test suite to ensure the success of the build</p>
<blockquote>
$ cd redis-stable<br>
$ make<br>
$ make test
</blockquote>

<p>Assuming the building and test suite were both successful, we can now make the Redis build available across the machine. The install script will prompt for some configuration values, pressing 'Enter' for each of them will confirm the suggested defaults.</p>
<blockquote>
$ sudo make install<br>
$ cd utils<br>
$ sudo ./install_server.sh
</blockquote>

<p>The completion of the script will start the Redis server, running as a background daemon on port 6379. Should you ever need to troubleshoot Redis, it will be helpful to start and stop the server using the following commands:</p>
<blockquote>
$ sudo service redis_6379 start<br>
$ sudo service redis_6379 stop
</blockquote> 

<h2 class="section-heading">Installing RVM</h2>
<p>RVM, or Ruby Version Manager is the package that allows for multiple local installs of ruby (and their corresponding gemsets) to exist alongside one another. It is the most convenient way to install Ruby, as well as get the Rails gem installed.</p>

<p>First, we need the public key to the machine hosting the RVM package. Let's download it:</p>
<blockquote>
$ gpg --keyserver hkp://keys.gnupg.net --recv-keys409B6B1796C275462A1703113804BB82D39DC0E3
</blockquote>

<p>RVM may now be installed using Curl:</p>
<blockquote>
$ \curl -sSL https://get.rvm.io | bash
</blockquote>

<p>The RVM install must now be sourced, making future terminal sessions aware of the package location</p>
<blockquote>
$ echo "source $HOME/.rvm/scripts/rvm" >> ~./bash_profile
</blockquote>
<p>*It is recommeded that you exit the current terminal session, and create a new session so that the 'rvm' package is sourced properly*</p>

<p>Lastly, lets use RVM to install Ruby version 2.2.3, and indicate to RVM that we would like the system to use Ruby version 2.2.3 by default</p>
<blockquote>
$ rvm install 2.2.3
$ rvm use 2.2.3
</blockquote>
