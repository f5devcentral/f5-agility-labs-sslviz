.. role:: red
.. role:: bred

Lab 3.3: Testing the Explicit Proxy deployment
----------------------------------------------

To test the deployed solution, RDP to the :bred:`Outbound Win7 Client` and do
the following:

.. hint:: Username = :red:`student` / Password = :red:`agility`

- Configure the client browser to use :red:`10.20.0.150:3128` for explicit
  proxy access.

  - This setting for Chrome can be find in :menuselection:`Settings -->
    Advanced --> Open proxy settings`.

- SSH to BIG-IP CLI and run the following tcpdump command to view the browser
  traffic hitting the explicit proxy IP.

  .. code-block:: bash

     tcpdump -nni client-net port 3128
  
- Test by browsing to url of choice.  You should see the traffic stream
  across tcpdump from previous command.

- An explicit proxy request test can also be done using command-line cURL:

  .. code-block:: bash

     curl -vk –proxy 10.20.0.150:3128 https://www.example.com

  Again watch the tcpdump from the previous test to confirm explicit proxy use.
