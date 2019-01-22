.. role:: red
.. role:: bred

.. image:: ../images/image11.png

Lab 1.7: Service Chain List
---------------------------

Service chains are arbitrarily-ordered lists of security devices. Based on
environmental requirements, different service chains may contain different
re-used sets of services, and different types of traffic can be assigned to
different service chains. For example, HTTP traffic may need to go through all
of the security services, while non-HTTP traffic goes through a subset, and
traffic destined to a financial service URL can bypass decryption and still
flow through a smaller set of security services.

  .. image:: ../images/image12.png

- Click :red:`Add` to create a new service chain containing all of the security
  services.

  - **Name** – provide a unique name to this service
    (ex.“:red:`my_service_chain`”).

  - **Services** – select any number of desired service and move them into the
    **Selected Service Chain Order** column, optionally also ordering them as
    required. In this lab, select :red:`all of the services`.

  - Click :red:`Save`.

- Click Add to create a new service chain for just the L2 (ex. FireEye) and TAP
  services.

  - **Name** – provide a unique name to this service (ex.
    “:red:`my_sub_service_chain`”).

  - **Services** – select the inline layer 2 (ex. FireEye) and TAP services.

  - Click :red:`Save`.

- Click :red:`Save & Next`.
