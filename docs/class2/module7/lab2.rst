.. role:: red
.. role:: bred

Lab 7.2: Deleting other objects
-------------------------------

While deleting a topology also removes its respective interception rules, it
does not remove the other objects - services, service chains, security policies
and SSL settings. These can all be removed individually, however must be
deleted in a hierarchical order. Once the topology and interception rules have
been deleted,

- SSL Settings can be deleted any time

- Delete any unused Security Policies

- Delete any unused Service Chains

- Delete any unused Services
