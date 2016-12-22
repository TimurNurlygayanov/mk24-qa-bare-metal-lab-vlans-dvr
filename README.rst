
================================================
mk24_qa_baremetal_vlan_dvr Reclass Model
================================================

Introduction
============
This repository contains salt model for QA bare-metal lab with MK24 Neutron OVS + VLANs + DVR.
All OpenStack controller nodes, nodes with BD and RabbitMQ clusters will be deployed on virtual machines (kvm01, kvm02 and kvm03),
all compute nodes and network gateway nodes will be bare-metal nodes.

config node
===========

cfg01

openstack control cluster
=========================

ctl01
ctl02
ctl03


salt model
=========================

To create new cluster use:

.. source-code:: bash

  ./reclass-clone.sh cluster.prod.region01 classes/system/openstack classes/system/linux/system classes/system/horizon/server classes/system/salt/control

  # Example:
  ./reclass-clone.sh cluster.region01 classes/system/openstack classes/system/linux/system classes/system/horizon/server classes/system/salt/control


To reclass existing tree use:

.. source-code:: bash

  ./reclass -h

  # move nodes under new cluster class
  ./reclass.sh system.linux.system cluster.region01 classes/system/reclass/storage/system/region01*

  # rename class definitions
  ./reclass.sh system.openstack system.openstack-mitaka classes/system/openstack/

  # update cluster classes with cluster preffix
  ./reclass.sh system.openstack cluster.region01 classes/cluster/region01/

  # update cluster classes with cluster preffix & rename class paths
  ./reclass.sh -r 's/openstack./openstack-mitaka./' system.openstack cluster.region03 classes/cluster/region03/system/openstack-mitaka/
