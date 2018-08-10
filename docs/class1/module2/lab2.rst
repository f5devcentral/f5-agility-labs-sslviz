Lab 2.2: Testing
----------------

#. Open up a RDP session to the Inbound Win7 Client and log using the documented credentials.

#. Launch Firefox and expand the :guilabel:`Inbound Testing`` Bookmarks

#. Use SSH or the console to the Layer 2 Security device and log in using the documented credentials.

   |image55|

#. Choose one of the Test websites and open the page.

#. Run a `tcpdump` with the following parameters:

      `sudo tcpdump -i eth5.60 -X`

   Refresh the web page in the browser and observe the plain text HTTP
   traffic in the Layer 2 Security device console.

   |image56|

.. |image55| image:: /_static/image51.png
   :width: 4.79167in
   :height: 2.93056in
.. |image56| image:: /_static/image40.png
   :width: 6.50000in
   :height: 2.63819in

