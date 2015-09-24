.. _check-queue-existence:

Check queue existence
^^^^^^^^^^^^^^^^^^^^^
.. code::

    GET /v1/{project_id}/queues/{queue_name}

This operation verifies whether the specified queue exists.

You can also use ``HEAD`` instead of ``GET`` for the verb.

The following table shows the possible response codes for this operation:

+--------------------------+-------------------------+-------------------------+
|Response Code             |Name                     |Description              |
+==========================+=========================+=========================+
|204                       |OK                       |The requested queue      |
|                          |                         |exists.                  |
+--------------------------+-------------------------+-------------------------+
|404                       |Not found                |The requested queue does |
|                          |                         |not exist.               |
+--------------------------+-------------------------+-------------------------+

Request
"""""""
The following table shows the URI parameters for the request:

+-------------+-------+------------------------------------------------------------+
|Name         |Type   |Description                                                 |
+=============+=======+============================================================+
|{project_id} |String |The project ID for the user. If you do not set the ``X-     |
|             |       |Project-Id header`` in the request, use ``project_id`` in   |
|             |       |the URI. For example: ``GET                                 |
|             |       |https://ord.queues.api.rackspacecloud.com/v1/{project_id}`` |
+-------------+-------+------------------------------------------------------------+
|{queue_name} |String |The name of the queue. ``queue_name`` is the name that you  |
|             |       |give to the queue. The name must not exceed 64 bytes in     |
|             |       |length, and it is limited to US-ASCII letters, digits,      |
|             |       |underscores, and hyphens.                                   |
+-------------+-------+------------------------------------------------------------+

.. note:: This operation does not accept a request body.

**Example Check queue existence: JSON request**

.. code::

   GET /v1/queues/demoqueue HTTP/1.1
   Host: ord.queues.api.rackspacecloud.com
   X-Project-Id: 806067


Response
""""""""
**Example Check queue existence: JSON response**


.. code::

   HTTP/1.0 204 OK
