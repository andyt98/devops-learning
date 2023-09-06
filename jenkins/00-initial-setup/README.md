**Initial Setup**

**Obs: Use a CentOS8 VM as a server, on which we run a Jenkins Docker
container**

docker run \--name jenkins_container -p 8080:8080 -p 50000:50000 -d -v
jenkins_home:/var/jenkins_home jenkins/jenkins:lts

to get the password from /var/jenkins_home/secrets/initialAdminPassword:

docker exec -it jenkins_container bash

**Settings to can access the Jenkins console at jenkins.local: \<port>
from host machine browser:**

On VM:

sudo firewall-cmd \--add-port=8080/tcp --permanent

sudo firewall-cmd --reload

to get the VM ip: sudo ifconfig

On Windows(host):

Command prompt -\> Run as administrator

notepad C:\\Windows\\System32\\drivers\\etc\\hosts

![](.//media/image1.png)

Install build tools in Jenkins:

![](.//media/image2.png)

Jenkins Plugin - In Global Tool Configuration:

![](.//media/image3.png)

Enter Jenkins container as root user:

docker exec -it -u 0 jenkins_container bash

to see Linux distribution: cat /etc/issue

apt update

apt install curl

Ex: To install npm and nodejs

curl -sL https://deb.nodesource.com/setup_10.x -o nodesource_setup.sh

bash nodesource_setup.sh

apt install nodejs

nodejs -v

npm -v

![](.//media/image4.png)

![](.//media/image5.png)

Install a tool on directly on Server: more difficult, but more flexible

Plugin: limited to provided input fields, depending on the plugin

2 ways to connect Jenkins to github repository using SSH:

1\. Get a terminal in Jenkins container and create a key there, then
connect it to github

2\. Using Credentials from Jenkins UI:

![](.//media/image6.png)

![](.//media/image7.png)

Enter the private key (cat \~/.ssh/id_rsa) of a SSH key already
connected to github

Jenkins store all its data in /var/jenkins_home

All jobs are stored in /var/jenkins_home/jobs

Git checkouts are stored in /var/jenkins_home/workspace

![](.//media/image8.png)
