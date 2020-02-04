.. role:: red
.. role:: bred

Step 4: Testing the deployment
==============================

To test the deployed solution, RDP to the :bred:`Outbound Client` and do
the following:

  .. hint:: Username = :red:`student` / Password = :red:`agility`

- Configure the client browser to use :red:`10.1.20.150:3128` for explicit
  proxy access.

  - This setting for Chrome can be found in :guilabel:`Settings \->
    Advanced \-> Open proxy settings`.

- SSH to the BIG-IP and run the following tcpdump command to view the browser
  traffic hitting the explicit proxy IP.

  .. code-block:: bash

     tcpdump -nni client-net port 3128

- Test by browsing to url of choice.  You should see the traffic stream
  across tcpdump from the previous command.

- An explicit proxy request can also be sent using command-line cURL:

  .. code-block:: bash

     curl -vk -proxy 10.20.0.150:3128 https://www.example.com

- Again watch the tcpdump from the previous test to confirm explicit proxy use.
