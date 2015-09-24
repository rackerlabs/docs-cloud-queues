.. _delete-message:

Delete message
^^^^^^^^^^^^^^
.. code::

    DELETE /v1/{project_id}/queues/{queue_name}/messages/{messageId}


This operation immediately deletes the specified message.

The ``claim_id`` parameter specifies that the message is deleted only if
it has the specified claim ID and that claim has not expired.
This specification is useful for ensuring only one worker processes any
given message. When a worker's claim expires before it can delete
a message that it has processed, the worker must roll back any actions
it took based on that message because another worker can now claim and
process the same message.

If you do not specify ``claim_id``, but the message is claimed,
the operation fails. You can only delete claimed messages by
providing an appropriate ``claim_id``.

The following table shows the possible response codes for this operation:

+--------------------------+-------------------------+-------------------------+
|Response Code             |Name                     |Description              |
+==========================+=========================+=========================+
|200                       |OK                       |The URI has invalid      |
|                          |                         |parameters. The invalid  |
|                          |                         |parameters are ignored.  |
+--------------------------+-------------------------+-------------------------+
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
|                          |                         |delete a message with an |
|                          |                         |expired claim ID.        |
+--------------------------+-------------------------+-------------------------+
|403                       |Forbidden                |An attempt was made to   |
|                          |                         |delete a message with    |
|                          |                         |non-existing claim ID.   |
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
|{messageId}  |String |The message ID.                                             |
+-------------+-------+------------------------------------------------------------+

The following table shows the query parameters for the request:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|claim_id                  |String *(Optional)*      |Identifies the claim.    |
+--------------------------+-------------------------+-------------------------+


.. note:: This operation does not accept a request body.


**Example Delete message: JSON request**


.. code::

   DELETE /v1/queues/demoqueue/messages/51db6f78c508f17ddc924358 HTTP/1.1
   Host: ord.queues.api.rackspacecloud.com
   Content-type: application/json
   X-Auth-Token: 0f6e9f63600142f0a970911583522217
   Client-ID: e58668fc-26eb-11e3-8270-5b3128d43830
   Accept: application/json
   X-Project-Id: 806067


Response
""""""""
**Example Delete message: JSON response**


.. code::

   HTTP/1.1 204 No Content
