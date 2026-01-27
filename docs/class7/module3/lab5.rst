Test the DoH Guardian Sinkhole Functionality
============================================

#. With everything configured, we will now test the DoH Guardian Sinkhole Functionality within a browser and the CLI.

#. Open the **Ubuntu-Client WEBRDP** session.

#. If the **Firefox** browser is not open, open it and navigate to ``https://www.f5.com``.

#. Observe that the browser is able to resolve the domain name and connect to the website.

#. Now let's navigate to a site that is categorized as *Sports* or *Entertainment*.

#. From the **Firefox** browser, navigate to the following URLs and observe the change that occur.

   .. code-block:: text

      https://www.nfl.com

   .. code-block:: text

      https://www.nbc.com

#. If setup correctly, the browser should display a blocking page.

   .. image:: images/doh-sinkhole-site-blocked.png
      :align: left


#. You can also test the DoH Guardian Sinkhole Functionality from the CLI.

#. Open the **Terminal Emulator** icon on the bottom menu.

   .. image:: images/doh-sinkhole-cli.png
      :align: left


#. Run the following commands (use Shift-Ctrl-V for Windows, and Option-Shift-Command-V for Mac) 

   .. code-block:: text

      curl -k --doh-insecure --doh-url https://dns.google/dns-query https://www.nbc.com

   .. code-block:: text

      curl -k --doh-insecure --doh-url https://dns.google/dns-query https://www.nfl.com

   .. note:: The --doh-insecure command requires Curl 7.76.1 and higher


#. If setup correctly, the CLI should display the blocking response.

   .. image:: images/doh-sinkhole-cli-blocked.png
      :align: left


Results & Additional Blocking Options
-------------------------------------

The result of both tests above should be the "Site Blocked!" page with a certificate forged by SSL Orchestrator. Injecting a static HTML response blocking page is just one option among many. You could, for example, issue a redirect instead of static HTML, and send the client to a more formal "splash page". This redirect could inject additional metadata to provide to the splash page. 

You would need to modify the ``sinkhole-target-rule`` iRule to issue a redirect instead of static HTML.

This is an example of a redirect to a splash page that includes additional metadata:

   .. code-block:: text

      when HTTP_REQUEST { HTTP::redirect "https://splash.f5labs.com/?cats=gis-dns-block&client_ip=[IP::client_addr]&type=dns&url=[URI::encode [b64encode [HTTP::host]]]" }

