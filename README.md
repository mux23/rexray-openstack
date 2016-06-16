# rexray-openstack
* support files for REX-Ray in OpenStack

In this repository you'll find supporting files for deploying a cluster of Docker servers using OpenStack Heat. These templates were created to support my talk at the OpenStack Summit in Austin, Texas in April 2016 - here is the abstract of that talk:

> **Persistent Storage For Containers Using Cinder**
> Everyone loves containers, but nobody wants to talk about the elephant in the room - how can you make storage persist when the whole point of containers is that they have short lifespans? In this presentation we'll discuss how to use the REX-Ray volume driver, backed by Cinder, to provide persistent, preemptable storage to Docker container servers hosted on OpenStack.

REX-Ray is a Docker volume drive plugin - it's really cool, and you can find it [here, on the EMC {code} github repo](https://github.com/emccode/rexray). Yay storage abstraction!

I used these files to deploy OpenStack on AWS, as a place to test the development of the Heat templates. If you use these files to deploy OpenStack on AWS, please know the following:
 - Nested virtualization is slow. Like, dog slow.
 - Deploying Docker means building a bunch of kernel-level stuff, and on nested virtualization this is **REALLY** slow.
 - I repeat: deploying Docker on a nested virtual machine, just using 'get.docker.io', takes like twelve hours. Not kidding.
 - To get any work done, a big AWS machine is necessary, like M4.4xlarge or something.
 - Deploying virtual machines inside OpenStack needs like 40G of space or something **per VM**. Remember that when deploying the AWS machine, since even M4.4xlarge only has like 50G of storage by default. Bump this up or get ready for failure.
 
###Usage
The two files here are:
- **heat_template.yaml** - a YAML file used as the template for the Heat system, and
- **local.conf** - a configuration file for DevStack that enables Heat and Neutron

The **local.conf** file will configure a fresh deployment of DevStack to use Heat, Ceilometer and Neutron networking, so that Heat orchestration templates can be developed and tested cleanly.
To use the local.conf file, download and install DevStack (following the instructions at http://docs.openstack.org/developer/devstack/). Place the local.conf file into the ./devstack directory, and launch DevStack using ./stack.sh.

The **heat_template.yaml** file will deploy four virtual machines - one 'master', and three worker nodes in an autoscaling group that technically should autoscale to five nodes under load, but I ran out of time on that part and didn't really test it or use that functionality in my talk. `¯\_(ツ)_/¯`

To use the Heat template, once DevStack is running, log into the Horizon dashboard and go to the 'Orchestration' tab, then click 'Stacks', and then 'Launch Stack' - when prompted for a template, point the file selector tool at the *heat_template.yaml* file.

A video of this stuff in action is available at https://www.youtube.com/watch?v=3MKCfp4XsiQ
