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

![](.//media/image2.png)
