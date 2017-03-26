# Docker Radius

- [Build radius docker image](#build-radius-docker-image)
- [Run radius docker container](#run-radius-docker-container)
- [Configure radius](#configure-radius)
- [Test radius](#test-radius)
- [Check radius log](#check-radius-log)

### Build radius docker image
    $ docker build -t radius .

### Run radius docker container
    $ docker-compose up -d

### Configure radius
    $ docker exec -it radius bash
    $ echo "testUser Cleartext-Password := \"testPassword\"" >> /etc/raddb/users 
    $ echo -e "client any {\n        ipaddr     = 0.0.0.0/0\n        secret    = testing123\n}" >> /etc/raddb/clients.conf
    $ exit
    $ docker restart radius 

### Test radius
    $ yum install -y freeradius-utils
    $ radtest testUser testPassword *<docker radius ip>* 0 testing123

### Check radius Log
    $ docker exec -it radius tail -f /tmp/radius.log
