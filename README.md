## Wrapper to deploy Rancher on Google Compute Engine
=====
Prerequisites:

- Google Cloud SDK - [SDK](https://cloud.google.com/sdk/)

=========
```
./gce-10acre-ranch -h
gce-10acre-ranch Usage:
    gce-10acre-ranch [opts]
    -a - Agent Container:
            needs full container repo/name[:tag]
    -c - Cluster name[Required]
    -d - DELETE ALL NODES
    -e - External IP for master...(yes this is getting rediculous)
    -i - Show the IP address of the master
    -h - Print this message
    -l - List nodes or clusters if no -c is passed
    -n - Number of nodes
    -s - Server Container:
            needs full container repo/name[:tag]
    -o - OS image
           centos-6 (Servers only. Configuration is manual)
           centos-7 (Servers only. Configuration is manual)
           rhel-6 (Servers only.)
           rhel-7 (Servers only.)
           coreos-alpha
           coreos-beta
           coreos-stable
           debian-7-backports
           fedora-21
           ubuntu
    -p - privileged
        - server
    -q - Do not prompt user
    -r - Registration url
    -w - Wait for a successful server ping
```

To set the GCE Project export the environment variable `GCE_PROJECT="<project>"`

To deploy a cluster:

```
./gce-10acre-ranch -c <clustername> [-n <number of nodes>]
```
`-n` is optional and defaults to 3.  Currently all nodes will be deployed with Ubuntu 14.04. The naming convention is:
<clustername>-10acre-master-0
<clustername>-10acre-[1:N]

For more customizations/testing capabilities you can sepecify the Docker images for server and agents:

```
Server
./gce-10acre-ranch -c <clustername> -n <number of nodes> -s rancher/server:development

Agent
./gce-10acre-ranch -c <clustername> -n <number of nodes> -a cloudnautique/agent:development

Or both
./gce-10acre-ranch -c <clustername> -n <number of nodes> -a cloudnautique/agent:development -s ibuildthecloud/dev-server
```
The Docker images must be real and accessible to Docker.





Get the master IP:

```
./gce-10acre-ranch -c <cluster name> -i
```
You can hit this IP over port 8080 to get to the UI

List all Clusters:

```
./gce-10acre-ranch -l
```
List all the nodes:

```
./gce-10acre-ranch -c <cluster name> -l
```

Destroy the cluster(-q for quiet):

```
./gce-10acre-ranch -c <cluster name> -d (-q)
```
