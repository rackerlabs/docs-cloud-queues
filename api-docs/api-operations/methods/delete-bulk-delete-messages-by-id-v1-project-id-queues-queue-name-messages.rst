.. _delete-bulk-messages-by-id:

^^^^^^^^^^^^^^^^^^^^^^^^^^
Bulk-delete messages by ID
^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    DELETE /v1/{project_id}/queues/{queue_name}/messages

This operation immediately deletes the specified messages. If any of
the message IDs are malformed or non-existent, they are ignored.
The remaining valid messages IDs are deleted.

The following table shows the possible response codes for this operation:

+--------------------------+-------------------------+-------------------------+
|Response Code             |Name                     |Description              |
+==========================+=========================+=========================+
|204                       |No content               |Success.                 |
+--------------------------+-------------------------+-------------------------+
|204                       |No content               |The request attempts to  |
|                          |                         |delete a message from a  |
|                          |                         |non-existing queue.      |
+--------------------------+-------------------------+-------------------------+
|204                       |No content               |The request attempts to  |
|                          |                         |delete a non-existing    |
|                          |                         |message.                 |
+--------------------------+-------------------------+-------------------------+
|400                       |Bad request              |The header has missing   |
|                          |                         |fields.                  |
+--------------------------+-------------------------+-------------------------+
|401                       |Unauthorized             |The request header has   |
|                          |                         |an invalid auth token.   |
+--------------------------+-------------------------+-------------------------+
|403                       |Forbidden                |An attempt was made to   |
|                          |                         |delete a claimed message |
|                          |                         |without providing a      |
|                          |                         |claim ID.                |
+--------------------------+-------------------------+-------------------------+
|403                       |Forbidden                |An attempt was made to   |
|                          |                         |delete messages with an  |
|                          |                         |expired claim ID.        |
+--------------------------+-------------------------+-------------------------+
|403                       |Forbidden                |An attempt was made to   |
|                          |                         |delete messages with non-|
|                          |                         |existing claim ID.       |
+--------------------------+-------------------------+-------------------------+
|406                       |Not acceptable           |The request header has   |
|                          |                         |Accept                   |
|                          |                         |!="application/json".    |
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

The following table shows the query parameters for the request:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|ids                       |String *(Required)*      |Specifies the IDs of the |
|                          |                         |messages to delete.      |
+--------------------------+-------------------------+-------------------------+

.. note:: This operation does not accept a request body.


**Example Bulk-delete messages by ID: JSON request**


.. code::

   DELETE /v1/queues/demoqueue/messages?ids=50b68a50d6f5b8c8a7c62b01,50b68a50d6f5b8c8a7c62b02 HTTP/1.1
   Host: ord.queues.api.rackspacecloud.com
   Content-type: application/json
   X-Auth-Token: 0f6e9f63600142f0a970911583522217
   Client-ID: e58668fc-26eb-11e3-8270-5b3128d43830
   Accept: application/json
   X-Project-Id: 806067


Response
""""""""
**Example Bulk-delete messages by ID: JSON response**


.. code::

   HTTP/1.1 204 No Content
