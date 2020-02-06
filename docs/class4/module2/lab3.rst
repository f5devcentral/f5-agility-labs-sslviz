.. role:: red
.. role:: bred

Testing the deployment
==============================

Gateway mode testing
--------------------

- For gateway mode testing, the lab's inbound desktop client includes
  static Hosts file entries that match the real IPs of the internal web server:

  10.1.10.90    test0.f5labs.com
  10.1.10.91    test1.f5labs.com
  10.1.10.92    test2.f5labs.com

  And a static persistent route that points 10.1.10.0/24 traffic to the BIG-IP
  outbound (external) VLAN self-IP (10.1.20.100).

  To test a **gateway mode** use case, open a web browser or cURL to one
  of the above URLs.

  .. code-block:: bash

     curl -vk https://test0.f5labs.com
     curl -vk https://test1.f5labs.com
     curl -vk https://test2.f5labs.com

Application mode testing
------------------------

- For application mode testing, create a static entry in /etc/hosts
  for:

  .. code-block:: bash

     10.1.20.120   www.f5labs.com

  To test an **application mode** use case, open a web browser or cURL to the
  above URL.

  .. code-block:: bash

     curl -vk https://www.f5labs.com
