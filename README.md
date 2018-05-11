Setting up a local PostgreSQL server in docker for testing
==========================================================

Use docker-compose to set up a postgresql docker and a pgadmin4 
docker. Use docker volume to create a docker volume which can 
be reused with other docker images if needed.


TLDR
----

    git clone https://github.com/magnus-lycka/mypg.git
    cd mypg
    docker volume create pg96data
    docker-compose up -d

Go to http://localhost/ and have fun...

    docker-compose down


Create docker volume for PostgreSQL 
-----------------------------------

You only need to do this once on the machine.

`$ docker volume create pg96data`


The docker images
-----------------

The docker images we use are described further here:

 * https://hub.docker.com/_/postgres/
 * https://hub.docker.com/r/dpage/pgadmin4/


The docker-compose config file
------------------------------

The file docker-compose.yml contains two services, the PostgreSQL
database service, `pg96`, and the web based PostgreSQL administration
service, `pgadmin4`.

I use `postgresql:9.6` since that's the version currently offered by AWS.
I expose the standard PostgreSQL port, but if that port is busy, change
to e.g. `15432:5432`.

PgAdmin4 is a nice web based admin GUI for PostgreSQL. I expose the
ordinary web port, but change to e.g. `8080:80` if port 80 is busy.


Starting and stopping the system
--------------------------------

Stand in the directory with the `docker-cmopose.yml` config file, and run


`$ docker-compose up -d`

or

`$ docker-compose down`


Using PgAdmin4
--------------

Log in to the PgAdmin4 GUI on http://localhost/ with the email and 
password given in the config file. If you changed port to e.g. `8080`,
you should go to http://localhost:8080/

 * Click on `Add New Server`.
 * In the `General` tab, you need to supply a name for the server to use as a label in PgAdmin4. 
 * In the `Connection` tab, you need to supply the hostname, which should be the same as the service name in `docker-compose.yml`, i.e. `pg96`.  The pre-filled username should be correct (`postgres`) unless you changed either either login in the config, but you need to supply the `POSTGRES_PASSWORD`.
 * Save!

The server should now by visible in the tree structure to the left.

