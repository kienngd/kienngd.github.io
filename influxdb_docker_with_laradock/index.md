# Influxdb Docker With Laradock


In this post we will see how to run influxdb docker container using laradock. Have fun.

InfluxDB docker document: [https://hub.docker.com/_/influxdb](https://hub.docker.com/_/influxdb)

Edit laradock **.env** file:

**Add these lines** at the end of file
```bash
### INFLUXDB ##################################################
# influxdb version, accept values: 1.7, 1.7.10, 1.8, 1.8.3, latest
INFLUXDB_VERSION=1.8
INFLUXDB_HTTP_PORT=8086
```

Edit **docker-composer.yml** file. Please remember to backup it first :).

**Add these lines** at the end of file
```bash
### influxdb ####################################################
influxdb:
  container_name: influxdb
  hostname: influxdb
  image: influxdb:${INFLUXDB_VERSION}
  ports:
    - "${INFLUXDB_HTTP_PORT}:8086"
  networks:
    - backend
  volumes:
    - ${DATA_PATH_HOST}/influxdb/var/lib/influxdb:/var/lib/influxdb
```

**Start influxdb container**
```bash
docker-composer up -d influxdb
```
<!--more-->
**Interact with data using influx command line**

-precision rfc3339 mean format time to human readable.
```bash
docker-compose exec influxdb influx -precision rfc3339
```

**API URI is**: http://localhost:8086
