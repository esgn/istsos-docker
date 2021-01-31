# istsos-docker

A Docker image for istSOS (http://istsos.org/)

Based on istSOS 2.3.3 and istSOS official tutorial data.

Tried and make it as light as possible. For demo/teaching purposes. Database content not persisted.

## Build and run

Clone and build the repository:
```
    $ git clone https://github.com/esgn/istsos-docker.git
    $ cd istsos-docker
    $ git checkout 2.3.3
    $ docker-compose up -d
```
istSOS admin interface will be available at http://localhost/istsos/admin.

Register database via istSOS web admin interface with the following information:
```
    user : pdm
    password : pdm
    host : istsos-db
    port : 5432
    database : istsos
```
## Proxy settings

Edit `docker-compose.yml` for setting your corporate proxy information. Uncomment and edit the `args` section of the istSOS image.


## Create ISTsos demo service

Follow the istSOS tutorial for [creating a new service instance](http://istsos.org/en/latest/doc/ws_instances.html#creating-a-new-service-instance). Use the name "demo" as stated in the tutorial. If you need the GRABOW procedure create it manually as stated in the istSOS tutorial.

## Create ISTsos demo procedures

Log into the istSOS container by creating a new instance of the container's shell.
```
    $ docker exec -ti istsos-2.3.3 /bin/sh
    / # cd /tmp/tutorial
    / # python fill/execute.py
    / # exit
```
## Insert sample data in demo procedures

Log into the istSOS container by creating a new instance of the container's shell.
```
    $ docker exec -ti istsos-2.3.3 /bin/sh
    / # cd /usr/local/istsos
    / # python scripts/csv2istsos.py -p BELLINZONA LOCARNO P_LUGANO T_LUGANO RH_GNOSCA -u http://localhost/istsos -s demo -w /tmp/dataset
    / # exit
```
You can add GRABOW to the command line if you've created it.
