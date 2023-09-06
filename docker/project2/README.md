**Project 2**

Notes about the Django app:

'DJANGO_LOCALDB' = 'true' => use local testing database

'DJANGO_LOCALDB' = 'false' => use remote database

![](.//media/image1.png)

The django app has hardocoded user, password and database used by
default when connecting to a remote database. THIS IS NOT RECOMMENDED IN
PRACTICE!

We will have to set the postgresql environment variables (from
<https://hub.docker.com/_/postgres> ) to these values

![](.//media/image2.png)

We have to name the postgresql service "db" because the value is
hardcoded. The remote database port is also hardcoded to the value 5432

Django app container port: 8000


**Create a Dockerfile tailored to run the web application:**

Use python:3 as base image

Set the appropriate environment variable to force the Django framework
to use a testing local sqlite3 database

Copy the repository content inside the container in /code folder

Set the working directory to /code

Install the requiements using pip as package manager

Use the following command to initialize the database and start the web
application:

python manage.py makemigrations && \\

python manage.py migrate && \\

python manage.py runserver 0.0.0.0:8000

![](.//media/image3.png)

Build the application and run it in background. Expose the port 20080 to
the outside world and link it to the local container socket
0.0.0.0:8000.

![](.//media/image4.png)

Access the application from the browser and play with it. Add a couple
of articles.

![](.//media/image5.png)
**Docker Compose**

Create a docker-compose file to support the following actions:

Call the corresponding service webapp

Build the container image

Set the environment variable to instruct the application to use the
local DB

Expose the application using port 20080

> ![](.//media/image6.png)
>
> ![](.//media/image7.png)

Run the docker compose in background and access the application

docker-compose up -d

> ![](.//media/image8.png)

Set the docker compose to down state

> ![](.//media/image9.png)

Add a new database service to your docker compose file

Use the latest official postgresql Docker image

Name the new service: db. We have to name the postgresql service "db"
because the value is hardcoded.

Check the official documentation from the DockerHub and set the
appropriate environment variables to match the values hardcoded within
the source code (settings.py)

We will have to set the postgresql environment variables (from
<https://hub.docker.com/_/postgres> ) to these values

![](.//media/image2.png)

Instruct the webservice to connect to the remote database instead of
local database (DJANGO_LOCALDB=false)

Ensure the webservice will be created after the database is up and
available (order matters!)

> ![](.//media/image10.png)

Run the docker compose in background and access the application

> ![](.//media/image11.png)
>
> ![](.//media/image12.png)

Set the docker compose to down state

> ![](.//media/image13.png)
**Docker Network**

Isolate the connection between database and webapp.

In order to enable the service discovery mechanism, docker compose deals
to create an isolated bridge network for the services listed within the
dockercompose.yml file. However, for extended control, one can specify
the network definition within the file, overriding the default behavior
with a custom, preferred one. For a better understanding, besides the
comprehensive documentation available here:
https://docs.docker.com/compose/ for the entire docker compose
mechanism, Docker community provides various samples and examples on how
to use their tools (here one can see that specific services may connect
to multiple isolated networks, since they are gates between different
scopes of the same distributed application - e.g.:
<https://github.com/dockersamples/example-voting-app/blob/master/dockercompose.yml>
)

Create a bridge network called journal-nw

Connect it to both services

> ![](.//media/image14.png)
>
> Run docker compose in background mode and access the application
>
> ![](.//media/image15.png)
>
> ![](.//media/image16.png)

Set the docker compose to down state

> ![](.//media/image17.png)

**Docker Volumes**

The application doesn't hold the database data between successive runs.
This behavior appears because, by design, a docker container is
volatile. In order to maintain the database content between successive
runs, one will need to mount a docker volume or a bind-mounted folder to
a specific path in the container context.

Check the postgres documentation from DockerHub, in order to identify
where postrgresql stores data by default.

PostgreSQL stores data by default in /var/lib/postgresql/data

Create a volume named journal-db in your docker compose file

Mount the volume to the specific path as suggested within the
documentation

> ![](.//media/image18.png)
>
> Run docker compose in background mode and access the application. Add
> some content to the journal/blog.

![](.//media/image19.png)

Set the docker compose to down state and make it up again. Access the
application. Is your previous content there?

![](.//media/image20.png)

The previous content is still there.
