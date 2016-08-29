.. _post-message:

Post message
~~~~~~~~~~~~

.. code::

    POST /v1/{project_id}/queues/{queue_name}/messages

This operation posts the specified message or messages.

You can submit up to 10 messages in a single request, but you must
always encapsulate the messages in a collection container
(an array in JSON, even for a single message - without the JSON array,
you receive the "Invalid request body" message). The resulting
value of the Location header or response body might be used to
retrieve the created messages for further processing.

The client specifies only the body and TTL for the message.
The server inserts metadata, such as ID and age.

The response body contains a list of resource paths that correspond
to each message submitted in the request, in the order of the messages.
If a server-side error occurs during the processing of the submitted
messages, a partial list is returned, the partial parameter is set
to true, and the client tries to post the remaining messages again.
If the server cannot enqueue any messages, the server returns
a ``503 Service Unavailable`` error message.

The ``body`` parameter specifies an arbitrary document that constitutes
the body of the message being sent.

The following rules apply for the maximum size:

* The maximum size of posted messages is the maximum size of the entire
  request document (rather than the sum of the individual message body
  field values as it was in earlier releases). On error, the
  client will now be notified of how much it exceeded the limit.
* The size is limited to 256 KB, including whitespace.

The document must be valid JSON. (|product name| validates it.)

The ``ttl`` parameter specifies how long the server waits before
marking the message as expired and removing it from the queue.
The value of ``ttl`` must be between 60 and 1209600 seconds (14 days).
Note that the server might not actually delete the message until
its age has reached up to (ttl + 60) seconds, to allow for
flexibility in storage implementations.

The following table shows the possible response codes for this operation:

+--------------------------+-------------------------+-------------------------+
|Response Code             |Name                     |Description              |
+==========================+=========================+=========================+
|200                       |OK                       |The URI might have       |
|                          |                         |invalid parameters, but  |
|                          |                         |the invalid parameters   |
|                          |                         |are ignored.             |
+--------------------------+-------------------------+-------------------------+
|201                       |Created                  |Success. With "partial": |
|                          |                         |true, multiple messages  |
|                          |                         |were posted in a single  |
|                          |                         |request and some of them |
|                          |                         |succeeded.               |
+--------------------------+-------------------------+-------------------------+
|400                       |Bad request              |An attempt was made to   |
|                          |                         |post more than 100       |
|                          |                         |messages with a single   |
|                          |                         |request.                 |
+--------------------------+-------------------------+-------------------------+
|400                       |Bad request              |An attempt was made to   |
|                          |                         |post with a TTL greater  |
|                          |                         |than 1209600.            |
+--------------------------+-------------------------+-------------------------+
|400                       |Bad request              |An attempt was made to   |
|                          |                         |post with a TTL less     |
|                          |                         |than 60.                 |
+--------------------------+-------------------------+-------------------------+
|400                       |Bad request              |An attempt was made to   |
|                          |                         |post with a negative     |
|                          |                         |value for TTL.           |
+--------------------------+-------------------------+-------------------------+
|400                       |Bad request              |An attempt was made to   |
|                          |                         |post with a non-JSON     |
|                          |                         |message.                 |
+--------------------------+-------------------------+-------------------------+
|400                       |Bad request              |An attempt was made to   |
|                          |                         |post with a non-integer  |
|                          |                         |value for TTL.           |
+--------------------------+-------------------------+-------------------------+
|400                       |Bad request              |An attempt was made to   |
|                          |                         |post with messages       |
|                          |                         |encapsulated in multiple |
|                          |                         |arrays.                  |
+--------------------------+-------------------------+-------------------------+
|400                       |Bad request              |An attempt was made to   |
|                          |                         |post with no request     |
|                          |                         |body.                    |
+--------------------------+-------------------------+-------------------------+
|400                       |Bad request              |An attempt was made to   |
|                          |                         |post with request body   |
|                          |                         |greater than 4 KB.       |
+--------------------------+-------------------------+-------------------------+
|400                       |Bad request              |An attempt was made to   |
|                          |                         |post without TTL in the  |
|                          |                         |request body.            |
+--------------------------+-------------------------+-------------------------+
|400                       |Bad request              |An attempt was made to   |
|                          |                         |post without the body    |
|                          |                         |parameter in request     |
|                          |                         |body.                    |
+--------------------------+-------------------------+-------------------------+
|400                       |Bad request              |The post request         |
|                          |                         |included a non-JSON body.|
+--------------------------+-------------------------+-------------------------+
|400                       |Bad request              |The post request         |
|                          |                         |included an invalid JSON |
|                          |                         |body.                    |
+--------------------------+-------------------------+-------------------------+
|400                       |Bad request              |The request header has   |
|                          |                         |missing fields.          |
+--------------------------+-------------------------+-------------------------+
|401                       |Unauthorized             |The request header has   |
|                          |                         |an invalid auth token.   |
+--------------------------+-------------------------+-------------------------+
|404                       |Not found                |An attempt was made to   |
|                          |                         |post a message to a non- |
|                          |                         |existing queue.          |
+--------------------------+-------------------------+-------------------------+
|406                       |Not acceptable           |The request header has   |
|                          |                         |Accept                   |
|                          |                         |!="application/json".    |
+--------------------------+-------------------------+-------------------------+
|429                       |Too many requests        |Too many requests.       |
+--------------------------+-------------------------+-------------------------+
|503                       |Service unavailable      |An attempt was made to   |
|                          |                         |post multiple messages   |
|                          |                         |in a single request and  |
|                          |                         |all of them failed.      |
+--------------------------+-------------------------+-------------------------+

Request
-------

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

**Example Post message: JSON request**

.. code::

   POST /v1/queues/demoqueue/messages HTTP/1.1
   Host: ord.queues.api.rackspacecloud.com
   Content-type: application/json
   Client-ID: e58668fc-26eb-11e3-8270-5b3128d43830
   X-Auth-Token: 0f6e9f63600142f0a970911583522217
   Accept: application/json
   X-Project-Id: 806067

.. code::

   [
      {
         "ttl":300,
         "body":{
            "event":"BackupStarted"
         }
      },
      {
         "ttl":60,
         "body":{
            "play":"hockey"
         }
      }
   ]

Response
--------

**Example Post message: JSON response**

.. code::

   HTTP/1.1 201 Created
   Content-Length: 149
   Content-Type: application/json; charset=utf-8
   Location: /v1/queues/demoqueue/messages?ids=51db6f78c508f17ddc924357,51db6f78c508f17ddc924358

.. code::

   {
      "partial":false,
      "resources":[
         "/v1/queues/demoqueue/messages/51db6f78c508f17ddc924357",
         "/v1/queues/demoqueue/messages/51db6f78c508f17ddc924358"
      ]
   }
