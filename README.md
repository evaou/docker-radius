[Build docker image](#build-docker-image)
[Run docker container](#Run docker container)
[Configure radius](#Configure radius)
[Restart docker container](#Restart docker container)
[Test radius](#Test Radius)
[Check radius log](#Check radius log)

## Build docker image
    $ docker build -t radius .

## Run docker container
    $ docker-compose up -d

## Configure radius
    $ docker exec -it radius bash
    $ echo "testUser Cleartext-Password := \"testPassword\"" >> /etc/raddb/users 
    $ echo -e "client any {\n        ipaddr     = 0.0.0.0/0\n        secret    = testing123\n}" >> /etc/raddb/clients.conf
    $ exit

##  Restart docker container
    $ docker restart radius 

## Test radius
    $ yum install -y freeradius-utils
    $ radtest testUser testPassword *<docker radius ip>* 0 testing123

## Check radius Log
    $ docker exec -it radius tail -f /tmp/radius.log
