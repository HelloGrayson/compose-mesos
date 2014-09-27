Run Mesos in Docker with Fig!

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

Let's launch a simple app like so:

```
curl -X POST -H "Accept: application/json" -H "Content-Type: application/json" \
  localdocker:8080/v2/apps -d '
{
    "id": "hello",
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
    },
    "volumes" : [
      {
        "containerPath": "/etc/a",
        "hostPath": "/var/data/a",
        "mode": "RO"
      },
      {
        "containerPath": "/etc/b",
        "hostPath": "/var/data/b",
        "mode": "RW"
      }
    ]
  },
  "id": "ubuntu",
  "instances": "1",
  "cpus": "0.1",
  "mem": "32",
  "uris": [],
  "cmd": "while sleep 10; do date -u +%T; done"
}'
```

Cheers!
