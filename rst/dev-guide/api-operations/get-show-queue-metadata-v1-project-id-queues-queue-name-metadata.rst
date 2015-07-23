
.. THIS OUTPUT IS GENERATED FROM THE WADL. DO NOT EDIT.

Show Queue Metadata
~~~~~~~~~~~~~~~~~~~~~~~~~

.. code::

    GET /v1/{project_id}/queues/{queue_name}/metadata

Shows metadata for the specified 				queue.

This operation returns metadata, such as message 				TTL, for the queue.



This table shows the possible response codes for this operation:


+--------------------------+-------------------------+-------------------------+
|Response Code             |Name                     |Description              |
+==========================+=========================+=========================+
|200                       |OK                       |Success, or no metadata  |
|                          |                         |exists for the queue, or |
|                          |                         |the URI has invalid      |
|                          |                         |parameters and the       |
|                          |                         |invalid parameters are   |
|                          |                         |ignored.                 |
+--------------------------+-------------------------+-------------------------+
|400                       |Bad request              |The request header has   |
|                          |                         |missing fields.          |
+--------------------------+-------------------------+-------------------------+
|401                       |Unauthorized             |The request header has   |
|                          |                         |an invalid auth token.   |
+--------------------------+-------------------------+-------------------------+
|404                       |Not found                |Metadata was requested   |
|                          |                         |for a queue that does    |
|                          |                         |not exist.               |
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








**Example Show Queue Metadata: JSON request**


.. code::

    GET /v1/queues/demoqueue/metadata HTTP/1.1
    Host: ord.queues.api.rackspacecloud.com
    Content-type: application/json
    X-Auth-Token: 0f6e9f63600142f0a970911583522217
    Accept: application/json
    X-Project-Id: 806067


Response
^^^^^^^^^^^^^^^^^^





**Example Show Queue Metadata: JSON response**


.. code::

    HTTP/1.1 200 OK
    Content-Length: 25
    Content-Type: application/json; charset=utf-8
    Content-Location: /v1/queues/demoqueue/metadata

