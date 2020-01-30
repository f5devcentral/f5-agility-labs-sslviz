Step 5: Modify the security policy to add the correct Service Chains
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  You should now be in the main **Configuration** section of the
   **SSL Orchestrator** main menu.

-  Select **Security Policies** from the list of options presented.

-  Select **ssloP\_f5labs\_explicit** from the list shown in the list.
   This should be the only selection on the list.

-  Click on the pencil icon next to the **Pinners\_Rule** |image16|

-  In the section shown below – click on menu selection for **Service
   Chain->ssloSC\_Cisco\_TAP** and press **OK.**

   |image17|

-  Repeat the same process for **Finance\_Bypass**

-  Now select **All Traffic** and select **ssloSC\_all\_devices**
   and press **OK**.

-  The screen should now look like the picture shown below.

   |image18|

-  Press **Deploy** and select **Ok** from the **Continue Save?**
   pop up menu.

-  Click on **Deploy**. This action will take a few seconds. Verify
   that the deployment was successful with no errors.

.. |image16| image:: ../media/image017.png
   :width: 0.22917in
   :height: 0.25000in
.. |image17| image:: ../media/image018.png
   :width: 4.45833in
   :height: 1.06250in
.. |image18| image:: ../media/image019.png
   :width: 7.05556in
   :height: 1.43681in
