Lab 1.8: Testing
----------------

In order to test the configuration, we will open an HTTPS website and
observe plain text traffic within the inspection zone.

Task 1 - Issuing Requests
~~~~~~~~~~~~~~~~~~~~~~~~~

1. Open a remote desktop (RDP) session to the Windows 7 Outbound Client
   and log in with the credentials referenced in the lab topology.

2. Open a web browser and navigate to some HTTPS URLs.

3. Observe the resigned certificate. (Pay attention to the Issued By line.)

   |image43|

4. SSH into the Layer 3 Security device with the credentials in the
   topology. Run a `tcpdump` with the following parameters:
 
      `sudo tcpdump -i eth5.60 -X`

   Observe the plain text HTTP traffic.

   |image44|

.. |image43| image:: /_static/image39.png
   :width: 6.50000in
   :height: 7.11250in
.. |image44| image:: /_static/image40.png
   :width: 6.50000in
   :height: 2.63819in

