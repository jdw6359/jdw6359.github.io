---
layout:     post
title:      "Rails REST API Setup"
subtitle:   "How to get up and running with the Particip8 application."
date:       2015-12-06 12:00:00
author:     "Josh Woodward"
header-img: "img/boba.jpg"
---

<p>This series of posts will assist you in getting the Particip8 application up and running. In this post, I will walk you through the steps needed to deploy the Rails component to the EC2 instance, in order to make the Particip8 REST API possible.</p>    
<h2 class="section-heading">Prerequisites</h2>
<p>Prior to setting up the rails application, we must make sure that we have the application prerequisites setup. The steps necessary to do this can be found here: <a href="https://jdw6359.github.io/2015/12/06/tools-setup/">Application Prerequisites</a></p> 

<h2 class="section-heading">Gem Dependencies</h2>
<p>The Ruby on Rails web application framework is dependent on several ruby gems, which can be installed (assuming a previously successful RVM install). The first; Bundler is a package that will be responsible for managing the application specific gems as well as managing and executing development and build tasks. Lets install bundler:
<blockquote>
$ gem install bundler
</blockquote>

<p>In order to install the 'Rails' gem, the Ubuntu 'libgmp-dev' package must be installed. Without it, Rails (and other application gems) will not be able to be downloaded and compiled properly</p>
<blockquote>
$ sudo apt-get install libgmp-dev
</blockquote>

<p>Lastly, let's install Rails! Rails can be easily installed as a Gem, just be patient! The download may take some time. Version 4.2.0 is stable, and will be installed by default</p>
<blockquote>
$ gem install rails
</blockquote>

<h2 class="section-heading">Cloning and Configuring the Application</h2>
<p>We can finally clone the Particip8 Rails repository. From the root of the EC2 instance, it is recommended that a 'source' directory be created. From there, you can clone the Particip8 Rails application</p>
<blockquote>
$ cd ~<br>
$ mkdir source<br>
$ cd source<br>
$ git clone https://github.com/BadgerHoneys/particip8.git 
</blockquote> 

<p>One of the gems, `mysql2` is dependent on a system package, `libmysqlclient-dev`, so we need to install it before installing the application gems</p>
<blockquote>
$ sudo apt-get install libmysqlclient-dev
</blockquote>

<p>In `particip8/Gemfile`, the application dependent gems can be installed with bundler</p>
<blockquote>
$ bundle install
</blockquote>

<p>Next, we must establish a connection to the MySQL database that was created earlier. In `config/database.yml`, edit the parameters for the `production` database to reflect the url, db username, and master password that were configured earlier</p>

<h2 class="section-heading">Using Nginx as a reverse proxy</h2>
<p>When we use bundler to run the rails server, it will run the server on port 3000. When external HTTP requests are made to the machine, they will come in on the default port for HTTP requests (port 80). With Nginx, requests to port 80 will be forwarded to the rails application on port 3000.</p>
<p>First, let's install nginx</p>
<blockquote>
$ sudo apt-get install nginx
</blockquote>

<p>Once installed, the operational rules for nginx can be defined. Navigate to `/etc/nginx` and open `default` in a terminal-based editor. Add the following to `default`:</p>
<blockquote>
<p>
server{
	
	listen 80;
	listen [::]:80;

	location /{
		proxy_pass http://localhost:3000
	}
}
</p>	

</blockquote>

<p>Lastly, we just need to restart the nginx service</p>
<blockquote>
$ sudo service restart nginx
</blockquote> 