##Docker Containers

 - Python 3
 - Nginx (SSL)
 - Postgresql

Step 1: Clone Repo

Step 2: Setup Env

    $ sudo vi .env

    # Add below Variables and changes value to your desire
    DEBUG=False
    TEMPLATE_DEBUG=False
    SECRET_KEY=yfehb3cr_(w9!&d&50f9n26^_je%4&eppxs1e2_@(*uof7nf-7
    DB_NAME=postgres
    DB_USER=postgres
    DB_PASS=postgres
    DB_SERVICE=postgres
    DB_PORT=5432
    THEME_VERSION=4.5.4

Step 3: Setup SSL Certificate
    https://www.digitalocean.com/community/tutorials/how-to-secure-nginx-on-ubuntu-14-04
    https://www.digitalocean.com/community/tutorials/how-to-create-an-ssl-certificate-on-nginx-for-ubuntu-14-04

Step 4: Configure docker-compose.yml

Step 5: Create Postgresql Database

    # Change postgres password (Security Reasons), Add User for the application
    $ psql -h 127.0.0.1 -p 5432 -U postgres --password
    postgres=# ALTER USER postgres WITH PASSWORD 'desired_password';
               CREATE DATABASE web;
               CREATE USER web WITH PASSWORD 'test';
               GRANT ALL PRIVILEGES ON DATABASE "web" to web;

Step 6: Clone django project repo


##Note:
###Postgres Backup

    $ docker exec -it suite_postgres_1 \
      sh -c "pg_dump -U postgres_user postgres_dbname | gzip > /postgres/backup/dump_`date +%d-%m-%Y"_"%H_%M_%S`.gz"

###Postgres Restore

    $ docker exec -it suite_postgres_1 \
        sh -c "gunzip -c /postgres/backup/filename.gz | psql -U postgres_user postgres_dbname"

###Handy Snippets

- KILL ALL DOCKER CONTAINER


    $ docker kill $(docker ps -a -q)

- REMOVE ALL DOCKER CONTAINER


    $ docker rm $(docker ps -a -q)

- LIST ACTIVE SERVICES


    $ netstat -tuplen
