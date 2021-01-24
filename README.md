# istsos-docker

A Docker image for istSOS (http://istsos.org/)

Based on istSOS 2.4.0-RC and istSOS official tutorial data.

Tried and make it as light as possible. For demo/teaching purposes. Database content not persisted.

## Build and run

Clone and build the repository:
```
    $ git clone https://github.com/psychicLocust/istsos-docker.git
    $ cd istsos-docker
    $ git checkout 2.4.0
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

Log into the istSOS container by creating a new instance of the container's shell.
```
    $ docker exec -ti istsos-2.4.0-RC4 /bin/sh
    / # cd /tmp/tutorial
    / # python3 fill/execute.py
    / # exit
```
## Insert sample data in demo service

Log into the istSOS container by creating a new instance of the container's shell.
```
    $ docker exec -ti istsos-2.4.0-RC4 /bin/sh
    / # cd /usr/local/istsos
    / # python3 scripts/csv2istsos.py -p BELLINZONA LOCARNO P_LUGANO T_LUGANO GRABOW RH_GNOSCA -u http://localhost/istsos -s demo -w /tmp/dataset
    / # exit
```