# emart-app

Launch an ubuntu EC2 instance with atleast t2.medium instance type and 20 GB SSD storage. Also, Make sure to allow traffic on port 22 and 80 from your source IP in inbound security group.

Run the following script in user-data script to install prerequistes:

-----------------------------------------------------

#!/bin/bash

sudo apt-get update
   sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release -y
   curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
   echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
  
   sudo apt-get update
   sudo apt-get install docker-ce docker-ce-cli containerd.io -y
   sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
   sudo chmod +x /usr/local/bin/docker-compose
   
    sudo usermod -a -G docker ubuntu
--------------------------------------------

Connect to EC2 instance using ssh client and clone this Github repository. Then, run the following commands to acess the application on port 80.

$ cd /emartapp
$ docker-compose build 
$ docker-compose up -d 

Copy and paste public IP of EC2 in web browser to access the emart app.
