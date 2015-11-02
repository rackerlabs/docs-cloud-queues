.. _get-messages-by-id:

^^^^^^^^^^^^^^^^^^
Get messages by ID
^^^^^^^^^^^^^^^^^^
.. code::

    GET /v1/{project_id}/queues/{queue_name}/messages

This operation provides a more efficient way to query multiple
messages compared to using a series of individual ``GET`` s.
Note that the list of IDs cannot exceed 20. If a malformed ID
or a nonexistent message ID is provided, it is ignored, and the
remaining messages are returned.

Unlike the get messages operation, a client's own messages are always
returned in this operation. If you use the ids parameter,
the echo parameter is not used and is ignored if it is specified.

The message body parameters are defined as follows:

* ``href`` is an opaque relative URI that the client can use to uniquely
  identify a message resource and interact with it.
* ``ttl`` is the TTL that was set on the message when it was posted.
  The message expires after (ttl - age) seconds.
* ``age`` is the number of seconds relative to the server's clock.
* ``body`` is the arbitrary document that was submitted with the
  original request to post the message.

The following table shows the possible response codes for this operation:

+--------------------------+-------------------------+-------------------------+
|Response Code             |Name                     |Description              |
+==========================+=========================+=========================+
|200                       |OK                       |Success. The URI might   |
|                          |                         |have invalid parameters, |
|                          |                         |but invalid parameters   |
|                          |                         |are ignored.             |
+--------------------------+-------------------------+-------------------------+
|400                       |Bad request              |An attempt was made to   |
|                          |                         |request messages with a  |
|                          |                         |limit greater than 100.  |
+--------------------------+-------------------------+-------------------------+
|401                       |Unauthorized             |The request header has   |
|                          |                         |an invalid auth token.   |
+--------------------------+-------------------------+-------------------------+
|404                       |Not found                |An attempt was made to   |
|                          |                         |request a message from a |
|                          |                         |non-existing queue.      |
+--------------------------+-------------------------+-------------------------+
|404                       |Not found                |An attempt was made to   |
|                          |                         |request messages with a  |
|                          |                         |limit less than or equal |
|                          |                         |to 0.                    |
+--------------------------+-------------------------+-------------------------+
|404                       |Not found                |An attempt was made to   |
|                          |                         |request messages with a  |
|                          |                         |non-boolean value for    |
|                          |                         |echo.                    |
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
|ids                       |String *(Optional)*      |Specifies the IDs of the |
|                          |                         |messages to get. Format  |
|                          |                         |multiple message ID      |
|                          |                         |values by separating     |
|                          |                         |them with commas (comma- |
|                          |                         |separated).              |
+--------------------------+-------------------------+-------------------------+

.. note:: This operation does not accept a request body.

**Example Get messages by ID: JSON request**

.. code::

   GET /v1/queues/demoqueue/messages?ids=51db6f78c508f17ddc924357,51db6ecac508f17ddc9242ad HTTP/1.1
   Host: ord.queues.api.rackspacecloud.com
   Content-type: application/json
   X-Auth-Token: 0f6e9f63600142f0a970911583522217
   Client-ID: e58668fc-26eb-11e3-8270-5b3128d43830
   Accept: application/json
   X-Project-Id: 806067

Response
""""""""
**Example Get messages by ID: JSON response**

.. code::

   HTTP/1.1 200 OK
   Content-Location: /v1/queues/fizbat/messages?ids=50b68a50d6f5b8c8a7c62b01,f5b8c8a7c62b0150b68a50d6

.. code::

   [
      {
         "href":"/v1/queues/fizbit/messages/50b68a50d6f5b8c8a7c62b01",
         "ttl":800,
         "age":32,
         "body":{
            "cmd":"EncodeVideo",
            "jobid":58229
         }
      },
      {
         "href":"/v1/queues/fizbit/messages/f5b8c8a7c62b0150b68a50d6",
         "ttl":800,
         "age":790,
         "body":{
            "cmd":"EncodeAudio",
            "jobid":58201
         }
      }
   ]
