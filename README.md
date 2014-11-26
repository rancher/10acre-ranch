# Wrapper around gcloud CLI to deploy rancher.
=====
Prerequisites:
Google Cloud SDK - [SDK](https://cloud.google.com/sdk/)

=========
```
./gce-10acre-ranch -h
gce-10acre-ranch Usage:
    gce-10acre-ranch [opts]
    -a - Agent Container:
            needs full container repo/name[:tag]
    -b - Build a new cluster
    -c - Cluster name[Required]
    -d - DELETE ALL NODES
    -i - Show the IP address of the master
    -h - Print this message
    -l - List nodes
    -n - Number of nodes
    -s - Server Container:
            needs full container repo/name[:tag]
```

To deploy a cluster:

```
./gce-10acre-ranch -c <clustername> -b -n <number of nodes>
```
Currently all nodes will be deployed with Ubuntu 14.04. The naming convention is:
<clustername>-10acre-master-0
<clustername>-10acre-[1:N]

For more customizations/testing capabilities you can sepecify the Docker images for server and agents:
```
# Server
./gce-10acre-ranch -c <clustername> -b -n <number of nodes> -s rancher/server:development
# Agent
./gce-10acre-ranch -c <clustername> -b -n <number of nodes> -a cloudnautique/agent:development
# Or both
./gce-10acre-ranch -c <clustername> -b -n <number of nodes> -a cloudnautique/agent:development -s ibuildthecloud/dev-server
```
The Docker images must be real and accessible to Docker.





Get the master IP:

```
./gce-10acre-ranch -c <cluster name> -i
```
You can hit this IP over port 8080 to get to the UI

List all the nodes:

```
./gce-10acre-ranch -c <cluster name> -l
```

Destroy the cluster:

```
./gce-10acre-ranch -c <cluster name> -d
```
