.. _claim-messages:

^^^^^^^^^^^^^^
Claim messages
^^^^^^^^^^^^^^
.. code::

    POST /v1/{project_id}/queues/{queue_name}/claims

This operation claims a set of messages (up to the value of the
``limit`` parameter) from oldest to newest and skips any messages
that are already claimed. If no unclaimed messages are available, the API
returns a ``204 No Content`` message.

When a client (worker) finishes processing a message, it should delete
the message before the claim expires to ensure that the message is
processed only once. As part of the delete operation,
workers should specify the claim ID (which is best done by simply
using the provided href). If workers perform these actions, then if a
claim simply expires, the server can return an error and notify
the worker of the race condition. This action gives the worker a
chance to roll back its own processing of the given message
because another worker can claim the message and process it.

The age given for a claim is relative to the server's clock. The claim's
age is useful for determining how quickly messages are getting
processed and whether a given message's claim is about to expire.

When a claim expires, it is released. If the original worker failed
to process the message, another client worker can then claim the message.

.. note::
   Claim creation is best-effort, meaning the worker
   may claim and return less than the requested number of messages.

The ``ttl`` parameter specifies how long the server waits before releasing
the claim. The ttl value must be between 60 and 43200 seconds (12 hours).
You must include a value for this parameter in your request.

The ``grace`` parameter specifies the message grace period in seconds.
The value of ``grace`` value must be between 60 and 43200 seconds (12 hours).
You must include a value for this parameter in your request.
To deal with workers that have stopped responding (for up to 1209600 seconds
or 14 days, including claim lifetime), the server extends the lifetime of
claimed messages to be at least as long as the lifetime of the
claim itself, plus the specified grace period. If a claimed message
would normally live longer than the grace period, its
expiration is not adjusted.

The following table shows the possible response codes for this operation:

+--------------------------+-------------------------+-------------------------+
|Response Code             |Name                     |Description              |
+==========================+=========================+=========================+
|201                       |Created                  |Success.                 |
+--------------------------+-------------------------+-------------------------+
|204                       |No content               |Success. A request was   |
|                          |                         |made to an empty queue   |
|                          |                         |with no messages to      |
|                          |                         |claim, or an attempt was |
|                          |                         |made to claim a message  |
|                          |                         |from a non-existing      |
|                          |                         |queue.                   |
+--------------------------+-------------------------+-------------------------+
|400                       |Bad request              |An attempt was made to   |
|                          |                         |claim a message using a  |
|                          |                         |non-JSON request body .  |
+--------------------------+-------------------------+-------------------------+
|400                       |Bad request              |An attempt was made to   |
|                          |                         |claim a message using a  |
|                          |                         |request with missing     |
|                          |                         |header fields.           |
+--------------------------+-------------------------+-------------------------+
|400                       |Bad request              |An attempt was made to   |
|                          |                         |claim a message using a  |
|                          |                         |request with no TTL      |
|                          |                         |parameter.               |
+--------------------------+-------------------------+-------------------------+
|400                       |Bad request              |An attempt was made to   |
|                          |                         |claim a message using a  |
|                          |                         |request with no request  |
|                          |                         |body.                    |
+--------------------------+-------------------------+-------------------------+
|400                       |Bad request              |An attempt was made to   |
|                          |                         |claim a message with an  |
|                          |                         |invalid TTL value (non-  |
|                          |                         |integer, or less than or |
|                          |                         |equal to 0).             |
+--------------------------+-------------------------+-------------------------+
|400                       |Bad request              |An attempt was made to   |
|                          |                         |claim a message with     |
|                          |                         |invalid JSON.            |
+--------------------------+-------------------------+-------------------------+
|400                       |Bad request              |An attempt was made to   |
|                          |                         |claim messages with an   |
|                          |                         |invalid value for limit  |
|                          |                         |(non-integer, or less    |
|                          |                         |than or equal to 0).     |
+--------------------------+-------------------------+-------------------------+
|400                       |Bad request              |An attempt was made to   |
|                          |                         |claim messages with the  |
|                          |                         |value of limit set to be |
|                          |                         |greater than 100.        |
+--------------------------+-------------------------+-------------------------+
|401                       |Unauthorized             |The request header has   |
|                          |                         |an invalid auth token.   |
+--------------------------+-------------------------+-------------------------+
|404                       |Not found                |An attempt was made to   |
|                          |                         |claim a message to a non-|
|                          |                         |existing queue.          |
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
|limit                     |Integer *(Optional)*     |Specifies the number of  |
|                          |                         |messages to return, up   |
|                          |                         |to 100 messages. If you  |
|                          |                         |do not specify a value   |
|                          |                         |for ``limit``, Cloud     |
|                          |                         |Queues claims 10         |
|                          |                         |messages. Once the       |
|                          |                         |messages are             |
|                          |                         |successfully claimed,    |
|                          |                         |Cloud Queues returns 10  |
|                          |                         |messages in the          |
|                          |                         |response. Messages are   |
|                          |                         |claimed based on the     |
|                          |                         |number of messages       |
|                          |                         |available. The server    |
|                          |                         |might claim and return   |
|                          |                         |less than the requested  |
|                          |                         |number of messages. If   |
|                          |                         |you specify a value for  |
|                          |                         |the limit parameter and  |
|                          |                         |the value is less than   |
|                          |                         |or equal to 100, Cloud   |
|                          |                         |Queues lets you claim    |
|                          |                         |free messages up to the  |
|                          |                         |number specified by the  |
|                          |                         |limit parameter. For     |
|                          |                         |example, if only 23      |
|                          |                         |messages are free and    |
|                          |                         |limit is 100, Cloud      |
|                          |                         |Queues claims all 23     |
|                          |                         |messages and returns 23  |
|                          |                         |messages in the          |
|                          |                         |response. If 120 free    |
|                          |                         |messages are available   |
|                          |                         |and limit is 100, Cloud  |
|                          |                         |Queues claims the oldest |
|                          |                         |100 messages and returns |
|                          |                         |100 messages in response.|
+--------------------------+-------------------------+-------------------------+

**Example Claim messages: JSON request**

.. code::

   POST /v1/queues/demoqueue/claims HTTP/1.1
   Host: ord.queues.api.rackspacecloud.com
   Content-type: application/json
   Client-ID: e58668fc-26eb-11e3-8270-5b3128d43830
   X-Auth-Token: 0f6e9f63600142f0a970911583522217
   Accept: application/json
   X-Project-Id: 806067

.. code::

   {
      "ttl":300,
      "grace":300
   }

Response
""""""""
**Example Claim messages: JSON response**

.. code::

   HTTP/1.1 201 OK
   Content-Length: 162
   Content-Type: application/json; charset=utf-8
   Location: /v1/queues/demoqueue/claims/51db7067821e727dc24df754

.. code::

   [
      {
         "body":{
            "event":"BackupStarted"
         },
         "age":239,
         "href":"/v1/queues/demoqueue/messages/51db6f78c508f17ddc924357?claim_id=51db7067821e727dc24df754",
         "ttl":300
      }
   ]
