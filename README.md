# rexray-openstack
* support files for REX-Ray in OpenStack

In this repository you'll find supporting files for deploying a cluster of Docker servers using OpenStack Heat. The two files of importance are:
- *heat_template.yaml* - a YAML file used as the template for the Heat system, and
- *local.conf* - a configuration file for DevStack that enables Heat and Neutron

To use the *local.conf* file, download and install DevStack (following the instructions at http://docs.openstack.org/developer/devstack/). Place the local.conf file into the ./devstack directory, and launch DevStack using ./stack.sh.

To use the Heat template, once DevStack is running, log into the Horizon dashboard and go to the 'Orchestration' tab, then click 'Stacks', and then 'Launch Stack' - when prompted for a template, point the file selector tool at the *heat_template.yaml* file.

A video of this in action is available at https://www.youtube.com/watch?v=3MKCfp4XsiQ
