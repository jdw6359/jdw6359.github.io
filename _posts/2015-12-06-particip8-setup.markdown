---
layout:     post
title:      "Setting up Particip8"
subtitle:   "How to get up and running with the Particip8 application."
date:       2015-12-06 12:00:00
author:     "Josh Woodward"
header-img: "img/boba.jpg"
---

<p>In this post, I will walk you through the installation steps necessary to get the Particip8 application up and running! You will be configuring EC2 and RDS instances on top of AWS's cloud as well as getting a Redis server, Rails web service, and Angular JS application deployed and running.</p>    

<h2 class="section-heading">Prerequisites</h2>
<p>Before you can instantiate machines on AWS's cloud, you must first have an AWS account. You can use the following link to access AWS's management application, and sign up for an account: https://aws.amazon.com/?nc2=h_lg. 

<h2 class="section-heading">Setting up Ubuntu 14.04 LTS Instance</h2>
<p>After logging into the AWS console, clicking into the EC2 link will bring up the EC2 Dashboard. The 'launch instance' button will provide a wizard, allowing users to configure the state of their new machine.</p>

<h3>Step 1: Choosing an Amazon Machine Image (AMI)</h3>
<p>In this portal you will have the option to choose the AMI that will be loaded onto your VM. Please select the 'Ubuntu Server 14.04 LTS (HVM)' AMI, and proceed to complete steps 2-5 by accepting the default values.

<h3>Step 6: Configuring Security Group</h3>
<p>This step will allow you to configure the allowed traffic in and out of the new machine. The only traffic that this machine will recognize is SSH and HTTP, both running on TCP, coming in on ports 22 and 80, respectively. In both cases, the traffic may originate from anywhere.</p>
<p>Add security rules for the traffic described above, and move to review the machine configuration.</p>

<h3>SSH Acccess</h3>
<p>Before the instance configuration can be finalized, an ssh key pair must be generated. AWS will prompt you to name the pair, as well as download the private key, to be stored on your local machine. The public portion will be saved on the new instance.</p>
<p>Once the instance has been configured and has started running, its ip and public dns are visible. To ssh into the instance, use the following command:
<blockquote>
$ ssh -i 'path/to/private.pem' ubuntu@'instance dns'
</blockquote>

<p>Once you are into the instance, you may want to update system packages:</p>
<blockquote>
$ sudo apt-get update
</blockquote>

<h2 class="section-heading">Setting up MySQL on RDS</h2>

<h2 class="section-heading">RVM and Rails</h2>

<h2 class="section-heading">Redis</h2>





<h2 class="section-heading">Prerequisites</h2>
<p>Cassandra relies on JDK 1.7, but it is acceptable to use a newer version such as JDK 1.8.</p>
<p>First, lets create a directory for our installation of the JDK to live</p>
<blockquote>
$ mkdir -p ~/opt/packages
</blockquote>




<blockquote>
$ sudo apt-get install default-jre
<br/>
$ java -v

</blockquote>

<blockquote>$ test</blockquote>

