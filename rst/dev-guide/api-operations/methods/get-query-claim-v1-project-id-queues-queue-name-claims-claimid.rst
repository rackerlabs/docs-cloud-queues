.. _get-query-claim:

Query claim
^^^^^^^^^^^
.. code::

    GET /v1/{project_id}/queues/{queue_name}/claims/{claimId}

This operation queries the specified claim for the specified queue.
Claims with malformed IDs or claims that are not found by ID are ignored.

The following table shows the possible response codes for this operation:

+--------------------------+-------------------------+-------------------------+
|Response Code             |Name                     |Description              |
+==========================+=========================+=========================+
|200                       |OK                       |Success. The request     |
|                          |                         |might have used invalid  |
|                          |                         |URI parameters, but      |
|                          |                         |invalid parameters were  |
|                          |                         |ignored.                 |
+--------------------------+-------------------------+-------------------------+
|400                       |Bad request              |The request had missing  |
|                          |                         |header fields.           |
+--------------------------+-------------------------+-------------------------+
|401                       |Unauthorized             |The request header has   |
|                          |                         |an invalid auth token.   |
+--------------------------+-------------------------+-------------------------+
|404                       |Not found                |The request included a   |
|                          |                         |claim from a non-        |
|                          |                         |existing queue.          |
+--------------------------+-------------------------+-------------------------+
|404                       |Not found                |The request included a   |
|                          |                         |non-existing claim ID.   |
+--------------------------+-------------------------+-------------------------+
|404                       |Not found                |The request included an  |
|                          |                         |expired claim.           |
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
|{claimId}    |String |The claim ID.                                               |
+-------------+-------+------------------------------------------------------------+

.. note:: This operation does not accept a request body.

**Example Query claim: JSON request**

.. code::

   GET /v1/queues/demoqueue/claims/51db7067821e727dc24df754 HTTP/1.1
   Host: ord.queues.api.rackspacecloud.com
   Content-type: application/json
   X-Auth-Token: 0f6e9f63600142f0a970911583522217
   Client-ID: e58668fc-26eb-11e3-8270-5b3128d43830
   Accept: application/json
   X-Project-Id: 806067

Response
""""""""
**Example Query claim: JSON response**

.. code::

   HTTP/1.1 200 OK
   Content-Length: 263
   Content-Type: application/json; charset=utf-8
   Content-Location: /v1/queues/demoqueue/claims/51db7067821e727dc24df754

.. code::

   {
     "age": 57,
     "href": "/v1/queues/demoqueue/claims/51db7067821e727dc24df754",
     "messages": [
       {
         "body": {
           "event": "BackupStarted"
         },
         "age": 296,
         "href": "/v1/queues/demoqueue/messages/51db6f78c508f17ddc924357?claim_id=51db7067821e727dc24df754",
         "ttl": 300
       }
     ],
     "ttl": 300
   }
   
