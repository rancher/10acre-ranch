# Wrapper around gcloud CLI to deploy rancher.
=====
```
./gce-10acre-ranch -h
gce-10acre-ranch Usage:
    gce-10acre-ranch [opts]
    -d - DELETE ALL NODES
    -i - Show the IP address of the master
    -h - Print this message
    -l - list nodes
    -n - number of nodes
```

To deploy a cluster:

```
./gce-10acre-ranch -n <number of nodes>
```
Currently all nodes will be deployed with Ubuntu 14.04. The naming convention is:
<user>-rancher-dev-master-0
<user>-rancher-dev-<1:N>


Get the master IP:

```
./gce-10acre-ranch -i
```
You can hit this IP over port 8080 to get to the UI

List all the nodes:

```
./gce-10acre-ranch -l
```

Destroy the cluster:

```
./gce-10acre-ranch -d
```