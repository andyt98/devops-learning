**Demo Freestyle Job:**

Created a jenkins-jobs branch on github and a simple script to run on
the freestyle job:

![](.//media/image1.png)

![](.//media/image2.png)

![](.//media/image3.png)

![](.//media/image4.png)

Created a test on jenkins-jobs branch

![](.//media/image5.png)

![](.//media/image6.png)

![](.//media/image7.png)

![](.//media/image8.png)

**Docker in Jenkins:**

Attaching a volume to Jenkins from the host file (on the host we have
docker available)

We are going to mount docker runtime directory from host into the
container as a volume, this will make docker available inside the
container

![](.//media/image9.png)

So we are going to kill our currently running container because we need
to start it again with additional volumes.

Because we have mounted volume to persist all the date in
/var/jenkins/home, on the host we still have the data. We can mount that
data into the new container.

![](.//media/image10.png)

![](.//media/image11.png)

![](.//media/image12.png)

Create jenkins container with mounted docker:

docker run \--name jenkins_container -p 8080:8080 -p 50000:50000 -d -v
jenkins_home:/var/jenkins_home -v
/var/run/docker.sock:/var/run/docker.sock -v \$(which
docker):/usr/bin/docker jenkins/jenkins:lts

Enter as root and modify docker.sock permission

docker exec -u 0 -it jenkins_container bash

chmod 666 /var/run/docker.sock

**Build Docker Image:**

Created a Dockerfile in github

![](.//media/image13.png)

![](.//media/image14.png)

![](.//media/image15.png)

![](.//media/image16.png)

**Next step:**

![](.//media/image17.png)

