.. _show-queue-stats:

^^^^^^^^^^^^^^^^
Show queue stats
^^^^^^^^^^^^^^^^
.. code::

    GET /v1/{project_id}/queues/{queue_name}/stats

This operation returns queue statistics, including how many messages
are in the queue, categorized by status.

.. note::
   If the value of the ``total`` parameter is 0, then ``oldest``
   and ``newest`` message statistics are not included in the response.

The following table shows the possible response codes for this operation:

+--------------------------+-------------------------+-------------------------+
|Response Code             |Name                     |Description              |
+==========================+=========================+=========================+
|200                       |OK                       |Success, or the URI has  |
|                          |                         |invalid parameters, but  |
|                          |                         |the invalid parameters   |
|                          |                         |are ignored.             |
+--------------------------+-------------------------+-------------------------+
|400                       |Bad request              |The request header has   |
|                          |                         |missing fields.          |
+--------------------------+-------------------------+-------------------------+
|401                       |Unauthorized             |The request header has   |
|                          |                         |an invalid auth token.   |
+--------------------------+-------------------------+-------------------------+
|404                       |Not found                |Stats were requested for |
|                          |                         |a queue that does not    |
|                          |                         |exist.                   |
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

.. note:: This operation does not accept a request body.

**Example Show queue stats: JSON request**

.. code::

   GET /v1/queues/demoqueue/stats HTTP/1.1
   Host: ord.queues.api.rackspacecloud.com
   Content-type: application/json
   X-Auth-Token: 0f6e9f63600142f0a970911583522217
   Accept: application/json
   X-Project-Id: 806067

Response
""""""""
**Example Show queue stats: JSON response**

.. code::

   HTTP/1.1 200 OK
   Content-Length: 53
   Content-Type: application/json; charset=utf-8
   Content-Location: /v1/queues/demoqueue/stats

.. code::

   {
      "messages":{
         "claimed":2409,
         "free":146929,
         "total":149338,
         "newest":{
            "age":12,
            "created":"2013-08-12T20:45:46Z",
            "href":"/v1/queues/fizbit/messages/50b68a50d6f5b8c8a7c62b01"
         },
         "oldest":{
            "age":63,
            "created":"2013-08-12T20:44:55Z",
            "href":"/v1/queues/fizbit/messages/50b68a50d6f5b8c8a7c62b01"
         }
      }
   }
