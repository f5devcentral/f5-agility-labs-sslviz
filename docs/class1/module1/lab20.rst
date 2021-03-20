.. role:: red
.. role:: bred

Test the new TAP service (optional - time permitting)
============================================================

One way to see if the security service is seeing decrypted traffic is to log into the 
console shell and run a  tcpdump capture on the
interface. A tcpdump capture usually requires *root* or *sudo* access.


Let's check if we see clear-text data on the TAP device.

-  In the UDF UI, select the :red:`Access` drop down selection on the :red:`Ubuntu18.04 Services` VM,
   then select :red:`WEB SHELL`.

-  In the web shell window, perform a packet capture using :red:`tcpdump`. The
   client machine's IP address is :red:`10.1.10.50`.

.. code-block:: bash

   sudo tcpdump -lnni eth1 -Xs0 host 10.1.10.50

-  Browse to an HTTPS web site (e.g., https://www.cnn.com) from the
   :red:`Ubuntu18.04 Client` machine (RDP session)
   and notice that the TAP device is receiving traffic unencrypted.

-  Return to the web shell and press :red:`<CTRL-C>` to stop the tcpdump.

.. ATTENTION::
   This is the end of the lab.
