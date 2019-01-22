.. role:: red
.. role:: bred

Lab 2.3: Testing
----------------

For gateway-mode testing, the lab’s inbound desktop client includes static
Hosts entries that match the *real* IPs of the internal web server:

- test0.f5demolabs.com = 10.20.0.90

- test1.f5demolabs.com = 10.20.0.91

- test3.f5demolabs.com = 10.20.0.92

And a static persistent route that points 10.1.10.0/24 traffic to the BIG-IP
outbound (external) VLAN self-IP (10.1.20.100). For targeted-mode testing,
create a static Hosts entry in /etc/hosts for:

  - `www.f5demolabs.com <http://www.f5demolabs.com>`__ = 10.30.0.200
