Run Mesos in Docker with Fig!

Assuming you've already [installed Fig](http://www.fig.sh/install.html), then running the following will boot up Mesos locally inside of Docker! Contribs welcome :)

```
fig up
```

Great! Now let's pop open the Mesos & Marathon UI's like so:

```
open http://localdocker:5050/ # open Mesos UI
open http://localdocker:8080/ # open Marathon UI
```

Finally, you can adjust the amount of slaves in your Mesos cluster like so:

```
fig scale slave=10
fig scale slave=1
```

Cheers!
