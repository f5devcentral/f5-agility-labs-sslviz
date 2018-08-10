Lab Topology
============

|image0|

|
| The credentials used to access the resources are:
|

.. list-table::
   :widths: 15 30 30
   :header-rows: 1
   :stub-columns: 1


   * - **Environment**
     - **Username**
     - **Password**
   * - Window(s) RDP
     - student
     - agility
   * - Ubuntu(s)
     - student
     - agility
   * - BIG-IP SSH
     - root
     - F5agility!2
   * - BIG-IP GUI
     - admin
     - F5agility!2

|
| And the networking information is as follows:
|

.. list-table::
   :widths: 15 30 30
   :header-rows: 1
   :stub-columns: 1


   * - **VLAN**
     - **Interface (tag)**
     - **Self-IP**
   * - client-net
     - 1.1
     - 10.20.0.100
   * - HTTP_in
     - 1.3 (110)
     - SSLO managed
   * - HTTP_out
     - 1.3 (120)
     - SSLO managed
   * - ICAP
     - admin
     - 10.70.0.10
   * - L2_in
     - 1.6
     - SSLO managed
   * - L2_out
     - 1.7
     - SSLO managed
   * - L3_in
     - 1.3 (50)
     - SSLO managed
   * - L3_out
     - 1.3 (60)
     - SSLO managed
   * - Tap
     - 1.4
     - SSLO managed
   * - outbound-net
     - 1.2
     - 10.30.0.100

.. |image0| image:: /_static/image0.png
    :width: 80%
