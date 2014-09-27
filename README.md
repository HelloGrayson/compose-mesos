![Fig Mesos](/../images/fig-mesos.jpg?raw=true "Fig Mesos")

#### Run Mesos in Docker with Fig!

Assuming you've already [installed Fig](http://www.fig.sh/install.html), then checkout and run:

```
fig start
```

To stream log output, simply run:

```
fig logs
```

Great! Now let's pop open the Mesos & Marathon UI's like so:

```
open http://localdocker:5050/ # open Mesos UI
open http://localdocker:8080/ # open Marathon UI
```

You can adjust the amount of slaves in your Mesos cluster like so:

```
fig scale slave=10
fig scale slave=1
```

Let's launch a simple app through [Marathon's REST API](https://mesosphere.github.io/marathon/docs/rest-api.html) like so:

```
curl -X POST -H "Accept: application/json" -H "Content-Type: application/json" \
  localdocker:8080/v2/apps -d '
{
    "id": "hello",
    "cpus": "0.1",
    "mem": "32",
    "cmd": "echo hello; sleep 10"
}'
```

And now for a Docker container:

```
curl -X POST -H "Accept: application/json" -H "Content-Type: application/json" \
  localdocker:8080/v2/apps -d '
{
    "container": {
        "type": "DOCKER",
        "docker": {
            "image": "libmesos/ubuntu"
        }
    },
    "id": "hello2",
    "instances": "1",
    "cpus": "0.1",
    "mem": "32",
    "uris": [],
    "cmd": "while sleep 10; do date -u +%T; done"
}'
```

Much thanks to the following sources:

* [An Introduction to Mesosphere](https://www.digitalocean.com/community/tutorials/an-introduction-to-mesosphere)
* [How To Configure a Production-Ready Mesosphere Cluster](https://www.digitalocean.com/community/tutorials/how-to-configure-a-production-ready-mesosphere-cluster-on-ubuntu-14-04)
* [Marathon v0.7.0 — Running Dockers at Scale and More](https://mesosphere.com/2014/09/25/marathon-0.7.0-released/)

Cheers!
