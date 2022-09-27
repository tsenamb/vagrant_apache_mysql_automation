# -*- mode: ruby -*-
# vi: set ft=ruby :
# v2.0
# Author: Joe Axberg
# Comment:  This vagrant file rocks

Vagrant.configure("2") do |config|
    
    #define a  do block for the web server 
    config.vm.define "web" do |web|
  
     #use the ubuntu/bionic64 VM template - it is the official Ubuntu one
     #if you want to use Ubuntu 20.04, replace bionic64 with focal64 
     web.vm.box = "ubuntu/bionic64"
 
     #setting up the networking such that the web server
     #will have two network adapters:  a NAT network with a port forward
     #to allow the outside world to connect to the server
     #and also a private "host only" network to allow the web server
     #to talk to the db server 
     web.vm.network "forwarded_port", guest: 80, host: 80
     web.vm.network "private_network", ip: "192.168.56.10"

     #set up a provision block and put in commands so that vagrant
     #installs the Apache web server
     #this block creates a script that will be run on the VM
     #the commands ran are between the <<-SHELL and SHELL
     # apt upgrade
 

     web.vm.provision "shell", inline: <<-SHELL
     #web provisioning goes here
     SHELL

    end   #end of the web server do block
  
    #another block that defines the db server.
    #we'll call it simply "db"
    config.vm.define "db" do |db|
  
     db.vm.box = "ubuntu/bionic64"
  
     #the VM will automatically get a NAT network connection
     #(outbound only) to get to the internet.
     #here connect the VM to the same private "host only" as
     #the web server
     db.vm.network "private_network", ip: "192.168.56.11"

     #stage the mysql config file, the line below will copy the file from your laptop
     #to the VM and put it in the /home/vagrant director (aka Vagrant's home directory)

     #add your awesome bash commands to install as much of a mysql
     #database server as you can
     db.vm.provision "shell", inline: <<-SHELL
     #db provisioning goes here
     SHELL
  
    end  #endof the db block
  
  end
