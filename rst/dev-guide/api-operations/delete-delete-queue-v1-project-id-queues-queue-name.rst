
.. THIS OUTPUT IS GENERATED FROM THE WADL. DO NOT EDIT.

Delete Queue
~~~~~~~~~~~~~~~~~~~~~~~~~

.. code::

    DELETE /v1/{project_id}/queues/{queue_name}

Deletes the specified queue.

This operation immediately deletes a queue and all 				of its existing messages.



This table shows the possible response codes for this operation:


+--------------------------+-------------------------+-------------------------+
|Response Code             |Name                     |Description              |
+==========================+=========================+=========================+
|200                       |OK                       |The URI has invalid      |
|                          |                         |parameters. The invalid  |
|                          |                         |parameters are ignored.  |
+--------------------------+-------------------------+-------------------------+
|204                       |No content               |Success.                 |
+--------------------------+-------------------------+-------------------------+
|204                       |No content               |Delete of a non-existing |
|                          |                         |queue.                   |
+--------------------------+-------------------------+-------------------------+
|400                       |Bad request              |The header has missing   |
|                          |                         |fields.                  |
+--------------------------+-------------------------+-------------------------+
|401                       |Unauthorized             |The request header has   |
|                          |                         |an invalid auth token.   |
+--------------------------+-------------------------+-------------------------+
|406                       |Not acceptable           |The request header has   |
|                          |                         |Accept                   |
|                          |                         |!="application/json".    |
+--------------------------+-------------------------+-------------------------+
|429                       |Too many requests        |Too many requests.       |
+--------------------------+-------------------------+-------------------------+


Request
^^^^^^^^^^^^^^^^^

This table shows the URI parameters for the request:

+-------------+-----------+------------------------------------------------------------+
|Name         |Type       |Description                                                 |
+=============+===========+============================================================+
|{project_id} |xsd:string |The project ID for the user. If you do not set the ``X-     |
|             |           |Project-Id header`` in the request, use ``project_id`` in   |
|             |           |the URI. For example: ``GET                                 |
|             |           |https://ord.queues.api.rackspacecloud.com/v1/{project_id}`` |
+-------------+-----------+------------------------------------------------------------+
|{queue_name} |xsd:string |The name of the queue. ``queue_name`` is the name that you  |
|             |           |give to the queue. The name must not exceed 64 bytes in     |
|             |           |length, and it is limited to US-ASCII letters, digits,      |
|             |           |underscores, and hyphens.                                   |
+-------------+-----------+------------------------------------------------------------+








**Example Delete Queue: JSON request**


.. code::

    DELETE /v1/queues/demoqueue HTTP/1.1
    Host: ord.queues.api.rackspacecloud.com
    Content-type: application/json
    X-Auth-Token: 0f6e9f63600142f0a970911583522217
    Accept: application/json
    X-Project-Id: 806067


Response
^^^^^^^^^^^^^^^^^^





**Example Delete Queue: JSON response**


.. code::

    HTTP/1.1 204 No Content

