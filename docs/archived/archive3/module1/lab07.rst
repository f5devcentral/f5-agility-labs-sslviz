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

- Click :guilabel:`Add` to create a new service chain containing all of the
  security services.

  - **Name** - provide a unique name to this service
    (ex.":red:`all_service_chain`").

  - **Services** - select any number of desired service and move them into the
    **Selected Service Chain Order** column, optionally also ordering them as
    required. In this lab, select :red:`all of the services` and then click the
    :guilabel:`rightward-pointing arrow` to move them to the Selected Service
    Chain Order side.

  - Click :guilabel:`Save`.

- Click :guilabel:`Add` to create a new service chain for just the L2 (ex.
  FireEye) and TAP services.

  - **Name** - provide a unique name to this service (ex.
    ":red:`sub_service_chain`").

  - **Services** - select and then move the :red:`FireEye` and :red:`TAP`
    services to the right-hand side.

  - Click :guilabel:`Save`.

- Click :guilabel:`Save & Next`.
