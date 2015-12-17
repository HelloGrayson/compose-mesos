#### Run Mesos in Docker with Docker Compose!

Assuming you've already [installed Docker Toolbox](https://www.docker.com/docker-toolbox), then checkout and run:

```
docker-compose up -d
```

To stream log output, simply run:

```
docker-compose logs
```

Great! Now let's pop open the Mesos, Marathon, & Chronos' UI like so:

```
open http://localdocker:5050/ # open Mesos UI
open http://localdocker:8080/ # open Marathon UI
open http://localdocker:4400/ # Open Chronos UI
```

Let's launch a simple app through [Marathon's REST API](https://mesosphere.github.io/marathon/docs/rest-api.html) like so:

```
curl -X POST -H "Accept: application/json" -H "Content-Type: application/json" \
  localdocker:8080/v2/apps -d '
{
    "id": "hello",
    "cpus": 0.1,
    "mem": 32,
    "cmd": "echo hello; sleep 10"
}'
```

And now for a Docker container:

```
curl -X POST -H "Accept: application/json" -H "Content-Type: application/json" \
  localdocker:8080/v2/apps -d '
{
    "id": "inky",
    "container": {
        "docker": {
            "image": "mesosphere/inky"
        },
        "type": "DOCKER",
        "volumes": []
    },
    "args": ["hello"],
    "cpus": 0.2,
    "mem": 32.0,
    "instances": 1
}'
```

Much thanks to the following sources:

* [An Introduction to Mesosphere](https://www.digitalocean.com/community/tutorials/an-introduction-to-mesosphere)
* [How To Configure a Production-Ready Mesosphere Cluster](https://www.digitalocean.com/community/tutorials/how-to-configure-a-production-ready-mesosphere-cluster-on-ubuntu-14-04)
* [Marathon v0.7.0 — Running Dockers at Scale and More](https://mesosphere.com/2014/09/25/marathon-0.7.0-released/)

Cheers!
