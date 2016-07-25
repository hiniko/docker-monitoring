Docker Monitor - Monitoring suite for your docker based insfrastucure
---------------------------------------------

This image contains a suite of software to monitor and graph your docker 
infrastructure. It intends to be an all in one image you can quickly start to
get monitoring up with as less hassle as possible (probably).

It contains `colelctd`, `statsd`, `graphite`, `carbon`  and `grafana`.
It also contains `dashbord-loader` to load dashboards droped in the `grafana`
directory into a running instance of `grafana`

The `collectd` instance montiors the host, by passing the host's /proc and using
the host's network stack.

There is an included grafana dashboard for the collectd instance.

## Configuration  ##

Configuraiton for each of the applicaitons lives in their named folder in this
repository. 

collectd uses a script at runtime to substitue envrioment variables in to the 
configuraiton. You can find these variables in the included docker-compose file.

### Building and using the image ###

There is a `docker-compose` file you can use to build and start the image:

`docker-compose build`

Grab a cup of tea. The first build takes a while.  If you change the image you 
should rebuild it, it will take less time to to chached steps

You also use the following to build and start the image:

`docker-compose up -d`

### Ports ###

The following ports are opened on the host:

* 8000 - Grafana
* 8001 - Graphite 
* 8125 - statsd 
* 8126 - statsd Admin
* 2003 - carbon data 
* 2004 - carbon pickle data

## Data  ##

Data is keep on the host in this repo and mounts are passed though to the
container. Remember to back this up!

## Logging and Management ##

Processes are managed by superviord 

Logs can be found in:
`/var/log/supervisord/<application>.log`

You can run the superviord shell by running:

```bash
$ docker exec -it docker-graphing supervisorctl 
carbon-cache                     RUNNING    pid 17, uptime 3:42:06 
collectd                         RUNNING    pid 15, uptime 3:42:06
dashboard-loader                 RUNNING    pid 19, uptime 3:47:03
grafana-webapp                   RUNNING    pid 9,  uptime 3:42:06
graphite-webapp                  RUNNING    pid 11, uptime 3:42:06
nginx                            RUNNING    pid 16, uptime 3:42:06
statsd                           RUNNING    pid 10, uptime 3:42:06
```

## Acknowledgements ##

This image was based off work from the following reops:

[docker-grafana-graphite](https://github.com/kamon-io/docker-grafana-graphite)
[collectd-container](https://github.com/rightscale/collectd-container)
[graphite_docker](https://github.com/SamSaffron/graphite_docker)

Personal work has been put in to include collectd to monitor the host and make
the default dashboards useful to those not using kamon.

## Author ##
Sherman Rose <sherman@shermanrose.uk>

## Licence ##
Licensed under the Apache 2.0 see LICENSE for more details

