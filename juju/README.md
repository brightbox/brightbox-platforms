# Juju 

[Juju](https://jujucharms.com/docs/stable/about-juju) is a
'state-of-the-art, open source, universal model for service oriented
architecture and service oriented deployments'.  The instructions and
scripts in this directory allow you to start a Juju cluster on the
[Brightbox Cloud](https://www.brightbox.com)

First make sure you have the [Brightbox CLI
installed](https://www.brightbox.com/docs/guides/cli/installation/)
and that it is [working with your Brightbox Account credentials](https://www.brightbox.com/docs/guides/cli/getting-started/). [Signing
Up](https://manage.brightbox.com/signup) is easy and you get trial credit
to get you started.

In particular make sure you have an [ssh key configured](https://www.brightbox.com/docs/guides/manager/ssh-keys/) and can log into servers with it. 

## Usage

You create a Juju cluster with the `build-cluster` script. This will build
a Juju Management Server from scratch, or it can be tailored to select the
[group](https://www.brightbox.com/docs/guides/cli/server-groups/) the
cluster will be part of, and the [server types](https://www.brightbox.com/docs/reference/server-types/) used for
both the management station and the cluster service machines.

## Build a Juju Cluster

`build-cluster` has several options:

```
build-cluster [-g server group] [-t server_type] [-m server_type]
  [-i cluster_size] [-n cluster_number]
```
* `server group` - The group id (in format grp-xxxxx) of the Juju Cluster
group you want to use instead of creating a new one. Useful if you've
already run the command before. Find it out by running `brightbox groups`
* `server type` - The type of server to add to the Juju cluster. Select
from the list obtained by running `brightbox types`. The default is a
`4gb.ssd` machine for a cluster machine [-t option] and `512mb.ssd` for the management station [-m option]
* `cluster size` - The number of cluster service machines to add to the cluster. Defaults to 0 so that only the management station is built. 
* `cluster number` - The identifier for this Juju Cluster. All brightbox
objects associated with the cluster are named with this identifier. The default is '1'. 

Run `build-cluster` with your chosen options and follow the onscreen
instructions.

## Using the Juju Cluster

Once the cluster is working you can refer to the [Using
the Juju GUI](https://jujucharms.com/docs/stable/howto-gui-management#using-the-gui) section of the Juju website to install
your applications and services onto the cluster.

You add additional cluster service machines to the cluster by
first creating servers with the Brightbox CLI, or [management
GUI](http://manage.brightbox.com), then add machines using the Juju CLI
from the management server.

```
juju add-machine srv-xxxxx
```

Repeat for every additional machine you want to add to the Juju cluster

## Cleaning up the Juju Cluster

The `cleanup-cluster` script can remove the entire Juju cluster and associated loadbalancers, groups, cloudips and images all in one go.

```
cleanup-cluster [-igc] cluster_domain/cip_id
```

* `cluster_domain/cip_id`: The domain or cloud ip id of the cluster to destroy: e.g: `cip-vsalc.gb1.brightbox.com` or just `cip-vsalc`.
* -g option removes the Juju group the cluster is in. 
* -c option removes the cloud ip completely rather than just unmapping it. 
