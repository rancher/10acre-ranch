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
    -c - Cluster name
    -d - DELETE ALL NODES
    -e - External IP for master...(yes this is getting rediculous)
    -i - Show the IP address of the master
    -h - Print this message
    -l - List nodes or clusters if no -c
    -n - Number of nodes [defaults to 3]
    -s - Server Container:
           needs full container repo/name[:tag]
    -o - OS Family
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
    -p - privileged agent (needed for Fedora)
    -q - Do not prompt user
    -r - Registration url
```

To set the GCE Project export the environment variable `GCE_PROJECT="<project>"`

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
./gce-10acre-ranch -c <clustername> -n <number of nodes> -s rancher/server:development

Agent
./gce-10acre-ranch -c <clustername> -n <number of nodes> -a cloudnautique/agent:development

Or both
./gce-10acre-ranch -c <clustername> -n <number of nodes> -a cloudnautique/agent:development -s ibuildthecloud/dev-server
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
### Contact
For bugs, questions, comments, corrections, suggestions, etc., open an issue in [rancherio/rancher](//github.com/rancherio/rancher/issues) with a title starting with `[10acre-ranch] `.

Or just [click here](//github.com/rancherio/rancher/issues/new?title=%5B10acre-ranch%5D%20) to create a new issue.

# License
Copyright (c) 2014-2015 [Rancher Labs, Inc.](http://rancher.com)

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

[http://www.apache.org/licenses/LICENSE-2.0](http://www.apache.org/licenses/LICENSE-2.0)

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

