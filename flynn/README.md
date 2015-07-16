# Flynn 

[Flynn](http://flynn.io) is a platform for running 'apps, databases,
websites and services at scale'. The instructions and scripts in this
directory allow you to start a Flynn cluster on the [Brightbox Cloud](https://www.brightbox.com)

First make sure you have the [Brightbox CLI
installed](https://www.brightbox.com/docs/guides/cli/installation/)
and that it is [working with your Brightbox Account credentials](https://www.brightbox.com/docs/guides/cli/getting-started/). [Signing
Up](https://manage.brightbox.com/signup) is easy and you get trial credit
to get you started.

In particular make sure you have an [ssh key configured](https://www.brightbox.com/docs/guides/manager/ssh-keys/) and can log into servers with it. 

## Usage

There are two scripts that can be used to generate a Flynn cluster: `build-cluster` and `build-image`.

* `build-cluster` on its own will build a three server Flynn
cluster from scratch, or it can be tailored to select the
[group](https://www.brightbox.com/docs/guides/cli/server-groups/),
[image](https://www.brightbox.com/docs/reference/server-images/) and
[server type](https://www.brightbox.com/docs/reference/server-types/)
* `build-image` creates a [server
snapshot](https://www.brightbox.com/docs/guides/cli/create-a-snapshot/)
with the Flynn software installed for faster Flynn cluster builds.

## Build a Flynn Image

Building a cluster from scratch can take a long time, so if you are using Flynn regularly it is a good idea to create an image so that clusters build much more quickly. 

Simply run `build-image` from the command prompt and it will create a
Flynn image for you automatically and register it in the [Image Library](https://www.brightbox.com/docs/guides/cli/image-library/). Make a note of the image id (in the format img-xxxxx) and specify it as an argument to `build-cluster`.

## Build a Flynn Cluster

`build-cluster` has several options:

```
build-cluster [-g server group] [-t server_type] [-i cluster_size] [-n cluster_number] [image_id]
```
* `server group` - The group id (in format grp-xxxxx) of the Flynn Cluster
group you want to use instead of creating a new one. Useful if you've
already run the command before. Find it out by running `brightbox groups`
* `server type` - The type of server to add to the Flynn cluster. Select
from the list obtained by running `brightbox types`. The default is a
`4gb.ssd` machine.
* `cluster size` - The number of servers you want in the cluster. Defaults
to 3 which is also the minimum size.
* `cluster number` - The identifier for this Flynn Cluster. All brightbox
objects associated with the cluster are named with this identifier. The default is '1'. 
* `image id` - The image id of the Flynn image built previously with
`build-image`. If you omit this argument `build-cluster` will build the cluster from scratch. 

Run `build-cluster` with your chosen options and follow the onscreen
instructions.

## Using the Flynn Cluster

Once the cluster is working you can refer to the [Using
Flynn](https://flynn.io/docs) section of the Flynn website to install
your applications and services onto the cluster.

## Cleaning up the Flynn Cluster

The 'cleanup-cluster' script can remove the entire Flynn cluster and associated loadbalancers, groups, cloudips and images all in one go.

```
cleanup-cluster [-igc] cluster_domain/cip_id
```

* `cluster_domain/cip_id`: The domain or cloud ip id of the cluster to destroy: e.g: `cip-vsalc.gb1.brightbox.com` or just `cip-vsalc`.
* -i option removes the Flynn image the cluster was built with.
* -g option removes the Flynn group the cluster is in. 
* -c option removes the cloud ip completely rather than just unmapping it. 


