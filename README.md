# openIMIS dockerized

 This repository provides a dockerized openIMIS (all components) as a quick setup for development, testing or demoing.
 

 Please look for further instructions on the openIMIS Wiki: https://openimis.atlassian.net/wiki/spaces/OP/pages/963182705/MO1.1+Install+the+modular+openIMIS+using+Docker

 
 The docker-compose currently contains the openIMIS database, backend + worker, frontend, restapi and gateway components.
 

In case of troubles, please consult/contact our service desk via our [ticketing site](https://openimis.atlassian.net/servicedesk/customer).

#Prerequisit
- Docker installed


# First startup

* create a `.env` file, use .env.example as starting point

## configure the restapi
 the rest api config files appsettings.json, appsettings.Production.json, appsetting.Developments.json must be created in the folder ./conf/restapi
 create the log folder ./logs¨

 to remove the restapi one will have to:
   - uncomment the volume in the fronend config
   - replace openimis.conf with openimis.conf.without_restapi

## configure the gateway (optionnal)
  
   - uncomment the volume in the fronend config
   - make modification in openimis.conf


## init database

by default the database is initialised with demo data without any action

# stop /start

To stop all docker containers: `docker-compose  stop`
To (re-)start all docker containers: `docker-compose  start` 

# pull new images

To pull new images or images update `docker-compose pull` 


# create lets encrypt certs

use the certbot docker compose file

export NEW_OPENIMIS_HOST first


## dry run 
docker-compose run --rm --entrypoint "  certbot certonly --webroot -w /var/www/certbot  --staging  --register-unsafely-without-email  -d  ${NEW_OPENIMIS_HOST}    --rsa-key-size 2048     --agree-tos     --force-renewal" certbot

## actual setup

docker-compose run --rm --entrypoint "  certbot certonly --webroot -w /var/www/certbot    --register-unsafely-without-email  -d  ${NEW_OPENIMIS_HOST}    --rsa-key-size 2048     --agree-tos     --force-renewal" certbot