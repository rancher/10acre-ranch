# Wrapper to deploy Rancher on Google Compute Engine or Docker for Mac

These scripts bootstrap a Rancher server and register one or more host node VMs to it.

- [Google Compute Engine](#google-compute-engine)
- [Docker for Mac Beta](#docker-for-mac-beta)

## Google Compute Engine

### Prerequisites

- Google Cloud SDK - [SDK](https://cloud.google.com/sdk/)

### Usage:
```
    gce-10acre-ranch [opts]
    -a - Agent Container:
            needs full container repo/name[:tag]
    -c - Cluster name [Required]
    -d - DELETE ALL NODES
    -e - External IP for master...(yes this is getting rediculous)
    -h - Print this message
    -i - Show the IP address of the master
    -l - List nodes or clusters if no -c is passed
    -m - Master Machine type (g1-small default)
    -M - Node Machine type (g1-small default)
    -n - Number of nodes [defaults to 3]
    -N - Network [default is default]
    -o - OS image
           centos-6 (Servers only. Configuration is manual)
           centos-7 (Servers only. Configuration is manual)
           rhel-6 (Servers only. Config is manual)
           rhel-7 (Servers only. Config is manual)
           coreos-<version>
           coreos (stable)
           debian-7-backports
           fedora-21 (Rancher Labs Only)
           ubuntu-<version>
    -p - privileged (needed for fedora)
        - server
        - agent
        - all
    -q - Do not prompt user
    -r - Registration url
    -s - Server Container:
            needs full container repo/name[:tag]
    -t - Test docker repos
    -z - Zone [us-central1-f default]
```

### If you are using this outside of Rancher Labs

Set the GCE Project via environment variable: ```GCE_PROJECT="<project>"```

### Images

For CoreOS and Ubuntu first look at the output of:

`gcloud compute images list --project <project>`

These versions do not always have aliases and update frequently. So we are just passing that along.

The default is Ubuntu-14-04 if no -o option is specified.

### To deploy a cluster:

```
./gce-10acre-ranch -c <clustername> -n <number of nodes>
```

### Deploy source code versions
```
gce-10acre-ranch -s rancher/build-master -p server -c rancher-dev -n 1
```

Currently all nodes will be deployed with Ubuntu 14.04. The naming convention is:
<clustername>-10acre-master-0
<clustername>-10acre-[1:N]

For more customizations/testing capabilities you can sepecify the Docker images for server and agents:

```
Server
./gce-10acre-ranch -c <clustername> -n <number of nodes> -s rancher/server:vX.Y.Z

Agent
./gce-10acre-ranch -c <clustername> -n <number of nodes> -a <user>/agent:vX.Y.Z

Or both
./gce-10acre-ranch -c <clustername> -n <number of nodes> -a <user>/agent:vX.Y.Z -s <user>/dev-server
```
The Docker images must be real and accessible to Docker.


### Get the master IP:

```
./gce-10acre-ranch -c <cluster name> -i
```
You can hit this IP over port 8080 to get to the UI

### List all Clusters:

```
./gce-10acre-ranch -l
```
### List all the nodes:

```
./gce-10acre-ranch -c <cluster name> -l
```

### Destroy the cluster(-q for quiet):

```
./gce-10acre-ranch -c <cluster name> -d (-q)
```

------
## Docker for Mac Beta

### Prerequisites

- Docker for Mac (http://beta.docker.com)

For additional hosts beyond the Docker for Mac VM:

- docker-machine-driver-xhyve (https://github.com/zchee/docker-machine-driver-xhyve)

### Usage
```
mac-ranch Usage:
    mac-ranch [opts]
    -c - Create world
    -d - Destroy world
    -h - Print this message
    -l - List hosts
    -r registration_url - Register another "-n" hosts using the given registration url

    -b - Boot2Docker URL (default: the one for v1.11.2)
    -i - No Inception - Prevent registering the Docker for Mac VM as a host
    -M - Host memory in mb (default: 1024)
    -n - Number of hosts (default: 0)
    -p - privileged (needed for build-master)
    -s - Server Container (default: rancher/server:latest)
            needs full container repo/name[:tag] 
    -u - Registry mirror URL (default: none)
```

### To deploy (single host):

```
./mac-ranch -c
```

#### A specific release
```
./mac-ranch -c -s rancher/server:vX.Y.Z
```

#### A build-master
```
./mac-ranch -c -p -s rancher/build-master
```

#### Multiple hosts
```
./mac-ranch -c -n <number of additional hosts>
```

### List all the hosts
```
./mac-ranch -l
```

### Destroy everything
```
./mac-ranch -d
```

### Contact
For bugs, questions, comments, corrections, suggestions, etc., open an issue in [rancher/rancher](//github.com/rancher/rancher/issues) with a title starting with `[10acre-ranch] `.

Or just [click here](//github.com/rancher/rancher/issues/new?title=%5B10acre-ranch%5D%20) to create a new issue.

# License
Copyright (c) 2014-2016 [Rancher Labs, Inc.](http://rancher.com)

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

[http://www.apache.org/licenses/LICENSE-2.0](http://www.apache.org/licenses/LICENSE-2.0)

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
