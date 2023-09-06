**Project 3 - Podman**

Search for the following information and store it in a file:

Search for a postgresql image in upstream using the Podman CLI tool.
Save the name of the bitnami image stored in quay.io.

Access the attached documentation and identify the keys for the
environment variables, used within the image to configure: the name of
the database, the username and the password.

Search for the official bitnami postrgresql container image repo and try
to identify the user id on whose behalf the database service will run in
the container. This information will be useful for persistence through
the bind mounting mechanism, to set the ownership of the folder shared
between the host system and container.

Check where the postgresql service stores data for persistence.

![](.//media/image1.png)

<https://github.com/bitnami/bitnami-docker-postgresql/blob/master/README.md>

<https://quay.io/repository/bitnami/postgresql>

The keys for the environment variables are: POSTGRESQL_DATABASE,
POSTGRESQL_PASSWORD and POSTGRESQL_USERNAME

The user id on whose behalf the database service will run in the
container is **1001.**

The postgresql service stores data for persistence in
/bitnami/postgresql

**Deploy the multi-service application with podman**

For simplicity, switch your current user to root (sudo su -- root)

Create an isolated bridge network called journal-nw using the podman CLI
tool.

![](.//media/image2.png)

Pull the postgresql bitmani image from Quay.io.

![](.//media/image3.png)

Create a /db folder. This folder will be further use for data
persistence. Instead of creating a volume, we will use the bind mounting
mechanism and we will share a folder between the container and the host
system.

Change the ownership to the userid indentified in the previous exercise.
The chown command is able to change ownership to a user id, even if that
ID does not yet exist on the system.

![](.//media/image4.png)

Run a postgresql container called db. See project-2 to see why it is so
important to name the service db.

Be sure to configure the database name and user credentials according to
the hardcoded configuration in the frontend (web service). You can
consult this quay.io repository:

<https://quay.io/repository/ioan_stan1/django-sample-docker-training>

Be sure you mount the /db folder to the appropriate path in order to
ensure persistence

Be sure you connect the db service to the newly provisioned network

Run the service in background with its own tty entity.

Run the web app and connect it to the database.

Be sure you connect the webapp service the newly provisioned networki n
order to be able to communicate with the database service

Enable remote database connection

Expose the application to the outside world using port TCP/20080
linkedto the inner socket running on port TCP/8000

Run the service in background with its own tty entity. Use the image
quay.io/ioan_stan1/django-sample-docker-training already built. Name
your container webapp.

podman run -dt \--name db \--network journal-nw -e
POSTGRESQL_USER=intern -e POSTGRESQL_DATABASE=blogpost -e
POSTGRESQL_PASSWORD=ship
\--mount=\"type=bind,src=/db,dst=/bitnami/postgresql\"
quay.io/bitnami/postgresql

podman run -dt -p 20080:8000 \--network journal-nw -e
DJANGO_LOCALDB=false \--name webapp
quay.io/ioan_stan1/django-sample-docker-training

![](.//media/image5.png)
