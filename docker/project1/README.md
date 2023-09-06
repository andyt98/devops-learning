**Crafting my own image**

Starting from ubuntu:20.04, create a Dockerfile

Install cowsay and fortune in ubuntu image via Dockerfile

Set the default image command to /usr/games/fortune \| /usr/games/cowsay

![](.//media/image1.png)

Build the image using the name my-cowsay with the tag v1.0

![](.//media/image2.png)

Run a container using the \--rm flag. This flag will delete the
container after executing the default command inside.

![](.//media/image3.png)

![](.//media/image4.png)

The RUN and CMD operations create 2 new layers on top of the base image.

The new image counts 4 layers, while the base image counts 2.

**CMD vs ENTRYPOINT**

Modify the Dockerfile and use /usr/games/cowthink as the unique CMD
value. Remove the fortune installation.

![](.//media/image5.png)

Build the image using the following tag my- cowthink:v1.0 and run it
using \--rm flag.

![](.//media/image6.png)

Try again but this time append the following string "echo hello" at the
end of your run command. What do you observe? What happens with your
Docker image default command when appending a string to your docker run
command?

![](.//media/image7.png)

The docker image default command when appending a string to the docker
run command is not executed, instead the new command is executed. The
CMD command is overwritten by docker running arguments.

Modify your Dockerfile and replace CMD with ENTRYPOINT.

![](.//media/image8.png)

Build the image using the tag my-cowthink:v2.0

![](.//media/image9.png)

Run a container using \--rm, first time with no extra arguments and
second time appending "echo hello". What do you observe?

![](.//media/image10.png)

![](.//media/image11.png)

ENTRYPOINT append the docker running argument as a string to the command
that is defined inside.

Modify your Dockerfile and replace append a CMD \["mooooo"\] command
immediately after ENTRYPOINT.

![](.//media/image12.png)

Build the image with the tag my-cowthink:v3.0
![](.//media/image13.png)


Run a container using \--rm, first time with no extra arguments and
second time appending "echo hello". What do you observe? What's the
behavior when using both ENTRYPOINT and CMD? How CMD can be used in
conjunction with ENTRYPOINT?

![](.//media/image14.png)

![](.//media/image15.png)

In conjunction with ENTRYPOINT, CMD can define a default value.

**Push image to upstream**

![](.//media/image16.png)

![](.//media/image17.png)

![](.//media/image18.png)
