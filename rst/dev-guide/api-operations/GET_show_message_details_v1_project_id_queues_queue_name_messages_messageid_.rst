=============================================================================
Show Message Details -  Queues
=============================================================================

Show Message Details
~~~~~~~~~~~~~~~~~~~~~~~~~

`Request <GET_show_message_details_v1_project_id_queues_queue_name_messages_messageid_.rst#request>`__
`Response <GET_show_message_details_v1_project_id_queues_queue_name_messages_messageid_.rst#response>`__

.. code-block:: javascript

    GET /v1/{project_id}/queues/{queue_name}/messages/{messageId}

Shows details for the specified message from the specified queue.

This operation shows details for the specified message from the specified queue.

If either the message ID is malformed or nonexistent, no message is returned.

Message body parameters are defined as follows: ``href`` is an opaque relative URI that the client can use to uniquely identify a message resource and interact with it. ``ttl`` is the TTL that was set on the message when it was posted. The message expires after (ttl - age) seconds. ``age`` is the number of seconds relative to the server's clock. ``body`` is the arbitrary document that was submitted with the original request to post the message.



This table shows the possible response codes for this operation:


+--------------------------+-------------------------+-------------------------+
|Response Code             |Name                     |Description              |
+==========================+=========================+=========================+
|200                       |OK                       |Success. The request     |
|                          |                         |found a matching         |
|                          |                         |message. The URI might   |
|                          |                         |have invalid parameters, |
|                          |                         |but the invalid          |
|                          |                         |parameters are ignored.  |
+--------------------------+-------------------------+-------------------------+
|400                       |Bad request              |The header has missing   |
|                          |                         |fields.                  |
+--------------------------+-------------------------+-------------------------+
|401                       |Unauthorized             |The request header has   |
|                          |                         |an invalid auth token.   |
+--------------------------+-------------------------+-------------------------+
|404                       |Not found                |An attempt was made to   |
|                          |                         |request a message from a |
|                          |                         |non-existing queue.      |
+--------------------------+-------------------------+-------------------------+
|404                       |Not found                |An attempt was made to   |
|                          |                         |request a non-existing   |
|                          |                         |message.                 |
+--------------------------+-------------------------+-------------------------+
|404                       |Not found                |An attempt was made to   |
|                          |                         |request an expired       |
|                          |                         |message.                 |
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
|{messageId}  |xsd:string |The message ID.                                             |
+-------------+-----------+------------------------------------------------------------+








**Example Show Message Details: JSON request**


.. code::

    GET /v1/queues/demoqueue/messages/51db6ecac508f17ddc9242ad HTTP/1.1
    Host: ord.queues.api.rackspacecloud.com
    Content-type: application/json
    X-Auth-Token: 0f6e9f63600142f0a970911583522217
    Client-ID: e58668fc-26eb-11e3-8270-5b3128d43830
    Accept: application/json
    X-Project-Id: 806067


Response
^^^^^^^^^^^^^^^^^^





**Example Show Message Details: JSON request**


.. code::

    HTTP/1.1 200 OK
    Content-Length: 126
    Content-Type: application/json; charset=utf-8
    Content-Location: /v1/queues/demoqueue/messages/51db6ecac508f17ddc9242ad

