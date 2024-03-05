# influxdb-v1-grafana system monitoring app 

Multi-container System monitoring with Grafana and Influxdb 

* [InfluxDB](https://github.com/influxdata/influxdb) - time series database
* [Chronograf](https://github.com/influxdata/chronograf) - admin UI for InfluxDB
* [Grafana](https://github.com/grafana/grafana) - visualization UI for InfluxDB

## Services

The services in Grafana run on the following ports:

| Host Port | Service |
| - | - |
| 3000 | [Grafana](http://127.0.0.1:3000) |
| 8086 | [InfluxDB](http://127.0.0.1:8086) |
| 8888 | [Chronograf](http://127.0.0.1:8888) |


## Quick Start

To start Grafana:

1. Run the following command:
```
docker-compose up -d
```

To stop Grafana:

1. Run the following command:
```
docker-compose down
```

## Chronograf tip
Note that Chronograf does not support username/password authentication. Anyone who can connect to the service has full admin access. Consequently, the service is not publically exposed and can only be access via the loopback interface on the same machine that runs docker.

If docker is running on a remote machine that supports SSH, use the following command to setup an SSH tunnel to securely access Chronograf by forwarding port 8888 on the remote machine to port 8888 on the local machine:

```
ssh [options] <user>@<docker-host> -L 8888:localhost:8888 -N
```

## Volumes

Grafana creates the following named volumes (one for each service) so data is not lost when Grafana is stopped:

* influxdb-storage
* chronograf-storage
* grafana-storage

## Users

Grafana creates two admin users - one for InfluxDB and one for Grafana. By default, the username and password of both accounts is `admin`. To override the default credentials, set the following environment variables before starting Grafana:

* `INFLUXDB_USERNAME`
* `INFLUXDB_PASSWORD`
* `GRAFANA_USERNAME`
* `GRAFANA_PASSWORD`

## Database

Grafana creates a default InfluxDB database called `db0`.
To change this you can
change the docker-compose.yml parameter INFLUXDB_DB=db0 

## Data Sources

Grafana will create a Grafana data source called `InfluxDB` that's connected to the default IndfluxDB database (e.g. `db0`).

To provision additional data sources: see the Grafana [documentation](http://docs.grafana.org/administration/provisioning/#datasources) and add a config file to `./grafana-provisioning/datasources/` before starting Grafana.

## Dashboards 

To add more dashboards: checkout the Grafana [documentation](http://docs.grafana.org/administration/provisioning/#dashboards) and add a config file to `./grafana-provisioning/dashboards/` before starting Grafana.
