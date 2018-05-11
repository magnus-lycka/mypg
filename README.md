Setting up a local Postgresql server in docker for testing
==========================================================

Use docker-compose to set up a postgresql docker and a pgadmin4 
docker. Use docker volume to create a docker volume which can 
be reused with other docker images if needed.


Create docker volume for Postgresql 
-----------------------------------

You only need to do this once on the machine.

$ docker volume create pg96data


The docker images
-----------------

The docker images we use are described further here:

 * https://hub.docker.com/_/postgres/
 * https://hub.docker.com/r/dpage/pgadmin4/


The docker-compose config file
------------------------------

The file docker-compose.yml contains two services, the postgresql
database service, pg96, and the web based postgresql administration
service, pgadmin4.

I use postgresql:9.6 since that's what's currently offered by AWS.
I expose the standard postgresql port, but if that port is busy, change
to e.g. 15432:5432.

As configured, the postgresql service allows you to log in as user
postgres with the password given in the config file. 

Pgadmin4 is a nice web based admin GUI for postgresql. I expose the
ordinary web port, but change to e.g. 8080:80 if port 80 is busy.
Log in to the Pgadmin4 GUI on localhost with the email and password
given in the config file.


Starting and stopping the system
--------------------------------

Stand in the directory with the docker-cmopose.yml config file, and run


$ docker-compose up -d

or

$ docker-compose down
