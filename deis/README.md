# Deis 

[Deis](http://deis.io) is is an open source PaaS that makes it easy to
deploy and manage applications on your own servers.  The instructions
and scripts in this directory allow you to start a Deis cluster on the
[Brightbox Cloud](https://www.brightbox.com)

First make sure you have the [Brightbox CLI
installed](https://www.brightbox.com/docs/guides/cli/installation/)
and that it is [working with your Brightbox Account credentials](https://www.brightbox.com/docs/guides/cli/getting-started/). [Signing
Up](https://manage.brightbox.com/signup) is easy and you get trial credit
to get you started.

In particular make sure you have an [ssh key configured](https://www.brightbox.com/docs/guides/manager/ssh-keys/) and can log into servers with it. 

## Usage

You generate a Deis cluster with the `build-cluster` script. This will build a three server Deis cluster from scratch, or it can be tailored to select the
[group](https://www.brightbox.com/docs/guides/cli/server-groups/) or 
[server type](https://www.brightbox.com/docs/reference/server-types/)

## Build a Deis Cluster

`build-cluster` has several options:

```
build-cluster [-g server group] [-t server_type] [-i cluster_size] [-n cluster_number]
```
* `server group` - The group id (in format grp-xxxxx) of the Deis Cluster
group you want to use instead of creating a new one. Useful if you've
already run the command before. Find it out by running `brightbox groups`
* `server type` - The type of server to add to the Deis cluster. Select
from the list obtained by running `brightbox types`. The default is a
`4gb.ssd` machine.
* `cluster size` - The number of servers you want in the cluster. Defaults
to 3 which is the minium size for a multi-server cluster.
* `cluster number` - The identifier for this Deis Cluster. All brightbox
objects associated with the cluster are named with this identifier. The default is '1'. 

Run `build-cluster` with your chosen options and follow the onscreen
instructions.

## Using the Deis Cluster

Once the cluster is working you can refer to the [Using
Deis](http://docs.deis.io/en/latest/using_deis/) section of the Deis website to install your applications and services onto the cluster.

## Cleaning up the Deis Cluster

The `cleanup-cluster` script can remove the entire Deis cluster and associated loadbalancers, groups, cloudips and images all in one go.

```
cleanup-cluster [-gc] cluster_domain/cip_id
```

* `cluster_domain/cip_id`: The domain or cloud ip id of the cluster to destroy: e.g: `cip-vsalc.gb1.brightbox.com` or just `cip-vsalc`.
* -g option removes the Deis group the cluster is in. 
* -c option removes the cloud ip completely rather than just unmapping it. 
