.. _using-cloud-queues:

Manage queues and process messages
------------------------------------

You can use the examples in the following sections to create message queues and process 
messages by using Cloud Queues API operations. Before running the examples, 
review the :ref:`Cloud Queues concepts<concepts>` to understand the 
API workflow, messaging patterns, and use cases.  

.. note:: 
     These examples use the ``$API_ENDPOINT``, ``$AUTH_TOKEN``, and ``$TENANT_ID`` environment 
     variables to specify the API endpoint, authentication token, and project ID values 
     for accessing the service. Make sure you 
     :ref:`configure these variables<configure-environment-variables>` before running the 
     code samples. 


.. include:: examples/gs-create-queue.rst
.. include:: examples/gs-post-message.rst
.. include:: examples/gs-claim-messages.rst
.. include:: examples/gs-delete-message.rst
.. include:: examples/gs-release-claim.rst
.. include:: examples/gs-delete-queue.rst

