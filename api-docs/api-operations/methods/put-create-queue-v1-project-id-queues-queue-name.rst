.. _create-queue:

^^^^^^^^^^^^
Create queue
^^^^^^^^^^^^
.. code::

    PUT /v1/{project_id}/queues/{queue_name}

This operation creates a new queue.

The following table shows the possible response codes for this operation:

+--------------------------+-------------------------+-------------------------+
|Response Code             |Name                     |Description              |
+==========================+=========================+=========================+
|201                       |Created                  |The request has been     |
|                          |                         |fulfilled and the queue  |
|                          |                         |was created.             |
+--------------------------+-------------------------+-------------------------+
|204                       |No content               |Success. The queue       |
|                          |                         |already exists.          |
+--------------------------+-------------------------+-------------------------+
|400                       |Bad request              |The queue has a long     |
|                          |                         |name (greater than 64    |
|                          |                         |bytes).                  |
+--------------------------+-------------------------+-------------------------+
|400                       |Bad request              |The request header has   |
|                          |                         |missing fields.          |
+--------------------------+-------------------------+-------------------------+
|401                       |Unauthorized             |The request header has   |
|                          |                         |an invalid auth token.   |
+--------------------------+-------------------------+-------------------------+
|429                       |Too many requests        |Too many requests.       |
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

**Example Create queue: JSON request**

.. code::

   PUT /v1/queues/demoqueue HTTP/1.1
   Host: ord.queues.api.rackspacecloud.com
   X-Auth-Token: 0f6e9f63600142f0a970911583522217
   Accept: application/json
   X-Project-Id: 806067

Response
""""""""
**Example Create queue: JSON response**

.. code::

   HTTP/1.1 201 Created
   Content-Length: 0
   Location: /v1/queues/demoqueue
