.. role:: raw-html(raw)
   :format: html

Step 3: Modify DNS settings to configure the AD server as DNS server (Lab only)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

*This step is required in this environment because of DHCP on the
   management interface. The DNS settings are modified to default DHCP
   settings periodically.*

*Usually the F5 devices IP addresses are managed manually and this step
   is not required.*

-  From the main menu select **System->Configuration->Device->DNS**
   and delete the **DNS Lookup Server List** and add the following IP
   address to the list :raw-html:`<i><font color="red">10.1.10.200</font></i>`. The configuration screen should
   look like the one shown below after the edit. 

-  Click **Update** at the bottom of the screen.

   |image36|

.. |image36| image:: ../media/image035.png
   :width: 7.05556in
   :height: 6.96528in
