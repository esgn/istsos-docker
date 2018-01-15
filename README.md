# istsos-docker

A Docker image for istSOS (http://istsos.org/)
Tried and make it as light as possible.
Based on istSOS 2.3.1 and istSOS official tutorial data.

## Build and run

Clone and build the repository:

    $ git clone https://github.com/psychicLocust/istsos-docker.git
    $ cd istsos-docker
    $ docker compose-up
    
istSOS admin interface will be available at http://localhost/istsos/admin. 
Register database with the following information:

    user : pdm
    password : pdm 
    host : postgis-db 
    port : 5432
    database : istsos

## Proxy settings

Edit `docker-compose.yml` for setting your corporate proxy information. Uncomment and edit the `args` section of the istSOS image.


## Create ISTsos demo service

Populate the istSOS instance with new service and offerings

    $ cd istsos-docker/tutorial
    $ python fill/execute.py
   
## Insert sample data in demo service

Log into the istSOS container by creating a new instance of the container's shell.

    $ docker exec -ti istsos_container_id /bin/sh
    # cd /usr/local/istsos
    # python scripts/csv2istsos.py -p BELLINZONA LOCARNO P_LUGANO T_LUGANO GRABOW RH_GNOSCA -u http://localhost/istsos -s demo -w /tmp/dataset
    # exit
