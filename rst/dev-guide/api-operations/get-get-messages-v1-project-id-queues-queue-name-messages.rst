
.. THIS OUTPUT IS GENERATED FROM THE WADL. DO NOT EDIT.

Get Messages
~~~~~~~~~~~~~~~~~~~~~~~~~

.. code::

    GET /v1/{project_id}/queues/{queue_name}/messages

Gets the message or messages in a 				specified queue.

This operation gets the message or messages in the 				specified queue.

Message IDs and markers are opaque strings. Clients 				should make no assumptions about their format or 				length. Furthermore, clients should assume that there 				is no relationship between markers and message IDs 				(that is, one cannot be derived from the other). This 				allows for a wide variety of storage driver 				implementations.

Results are ordered by age, oldest message first.

A request to list messages when the queue is not 				found or when messages are not found returns 204, 				instead of 200, because there was no information to 				send back. Messages with malformed IDs or messages 				that are not found by ID are ignored.



This table shows the possible response codes for this operation:


+--------------------------+-------------------------+-------------------------+
|Response Code             |Name                     |Description              |
+==========================+=========================+=========================+
|200                       |OK                       |Success. One or more     |
|                          |                         |messages were found. The |
|                          |                         |request might have       |
|                          |                         |included an invalid      |
|                          |                         |parameter (something     |
|                          |                         |other than marker,       |
|                          |                         |limit, echo, or          |
|                          |                         |include_claimed).        |
+--------------------------+-------------------------+-------------------------+
|204                       |No content               |Success, but no messages |
|                          |                         |matched the request. Or, |
|                          |                         |a message with a non-    |
|                          |                         |existing marker was      |
|                          |                         |requested.               |
+--------------------------+-------------------------+-------------------------+
|204                       |No content               |A message with a non-    |
|                          |                         |existing marker was      |
|                          |                         |requested.               |
+--------------------------+-------------------------+-------------------------+
|400                       |Bad request              |An attempt was made to   |
|                          |                         |request messages with a  |
|                          |                         |limit greater than 100.  |
+--------------------------+-------------------------+-------------------------+
|400                       |Bad request              |An attempt was made to   |
|                          |                         |request messages with a  |
|                          |                         |limit less than or equal |
|                          |                         |to 0.                    |
+--------------------------+-------------------------+-------------------------+
|400                       |Bad request              |An attempt was made to   |
|                          |                         |request messages with a  |
|                          |                         |non-boolean value for    |
|                          |                         |echo.                    |
+--------------------------+-------------------------+-------------------------+
|401                       |Unauthorized             |The request header has   |
|                          |                         |an invalid auth token.   |
+--------------------------+-------------------------+-------------------------+
|404                       |Not found                |An attempt was made to   |
|                          |                         |request a message from a |
|                          |                         |non-existing queue.      |
+--------------------------+-------------------------+-------------------------+
|406                       |Not acceptable           |The request header has   |
|                          |                         |Accept                   |
|                          |                         |!="application/json".    |
+--------------------------+-------------------------+-------------------------+
|429                       |Too many requests        |Too many requests.       |
+--------------------------+-------------------------+-------------------------+
|503                       |Service unavailable      |The server is currently  |
|                          |                         |unavailable.             |
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



This table shows the query parameters for the request:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|marker                    |xsd:string *(Required)*  |Specifies an opaque      |
|                          |                         |string that the client   |
|                          |                         |can use to request the   |
|                          |                         |next batch of messages.  |
|                          |                         |The ``marker`` parameter |
|                          |                         |communicates to the      |
|                          |                         |server which messages    |
|                          |                         |the client has already   |
|                          |                         |received. If you do not  |
|                          |                         |specify a value, the API |
|                          |                         |returns all messages at  |
|                          |                         |the head of the queue    |
|                          |                         |(up to the limit).       |
+--------------------------+-------------------------+-------------------------+
|limit                     |xsd:integer *(Required)* |When more messages are   |
|                          |                         |available than can be    |
|                          |                         |returned in a single     |
|                          |                         |request, the client can  |
|                          |                         |pick up the next batch   |
|                          |                         |of messages by simply    |
|                          |                         |using the URI template   |
|                          |                         |parameters returned from |
|                          |                         |the previous call in the |
|                          |                         |"next" field. Specifies  |
|                          |                         |up to 10 messages (the   |
|                          |                         |default value) to        |
|                          |                         |return. If you do not    |
|                          |                         |specify a value for the  |
|                          |                         |limit parameter, the     |
|                          |                         |default value of 10 is   |
|                          |                         |used.                    |
+--------------------------+-------------------------+-------------------------+
|echo                      |xsd:boolean *(Required)* |Determines whether the   |
|                          |                         |API returns a client's   |
|                          |                         |own messages. The        |
|                          |                         |``echo`` parameter is a  |
|                          |                         |Boolean value (``true``  |
|                          |                         |or``false``) that        |
|                          |                         |determines whether the   |
|                          |                         |API returns a client's   |
|                          |                         |own messages, as         |
|                          |                         |determined by the        |
|                          |                         |``uuid`` portion of the  |
|                          |                         |User-Agent header. If    |
|                          |                         |you do not specify a     |
|                          |                         |value,``echo`` uses the  |
|                          |                         |default value            |
|                          |                         |of``false``. If you are  |
|                          |                         |experimenting with the   |
|                          |                         |API, you might want to   |
|                          |                         |set``echo=true`` in      |
|                          |                         |order to see the         |
|                          |                         |messages that you posted.|
+--------------------------+-------------------------+-------------------------+
|include_claimed           |xsd:boolean *(Required)* |Determines whether the   |
|                          |                         |API returns claimed      |
|                          |                         |messages and unclaimed   |
|                          |                         |messages.                |
|                          |                         |The``include_claimed``   |
|                          |                         |parameter is a Boolean   |
|                          |                         |value (``true``          |
|                          |                         |or``false``) that        |
|                          |                         |determines whether the   |
|                          |                         |API returns claimed      |
|                          |                         |messages and unclaimed   |
|                          |                         |messages. If you do not  |
|                          |                         |specify a value,         |
|                          |                         |``include_claimed`` uses |
|                          |                         |the default value of     |
|                          |                         |``false`` (only          |
|                          |                         |unclaimed messages are   |
|                          |                         |returned).               |
+--------------------------+-------------------------+-------------------------+







**Example Get Messages: JSON request**


.. code::

    GET /v1/queues/demoqueue/messages?echo=true HTTP/1.1 
    Host: ord.queues.api.rackspacecloud.com
    Content-type: application/json 
    Client-ID: e58668fc-26eb-11e3-8270-5b3128d43830
    X-Auth-Token: 0f6e9f63600142f0a970911583522217
    Accept: application/json
    X-Project-Id: 806067


Response
^^^^^^^^^^^^^^^^^^





**Example Get Messages: JSON response**


.. code::

    HTTP/1.1 204 No Content

