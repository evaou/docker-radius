# Docker Radius 

1. Build docker image

    $ docker build -t radius .

# Run docker container

    $ mkdir -p /tmp/var/log/radius
    $ docker-compose up -d

# Configure radius

    $ docker exec -it radius bash
    $ echo "testing Cleartext-Password := \"password\"" >> /etc/raddb/users 
    $ echo -e "client any {\n        ipaddr     = 0.0.0.0/0\n        secret    = testing123\n}" >> /etc/raddb/clients.conf
    $ exit

#  Restart docker container

    $ docker restart radius 

# Test Radius

    $ yum install -y freeradius-utils
    $ radtest testing password <docker radius ip> 0 testing123

# Check Radius Log

    $ docker exec -it radius tail -f /var/log/radius/radius.log
