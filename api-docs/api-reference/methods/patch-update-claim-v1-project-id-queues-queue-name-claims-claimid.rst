.. _patch-update-claim:

Update claim
~~~~~~~~~~~~

.. code::

    PATCH /v1/{project_id}/queues/{queue_name}/claims/{claimId}

This operation updates the specified claim for the specified queue.
Claims with malformed IDs or claims that are not found by ID are ignored.

Clients should periodically renew claims during long-running batches
of work to avoid losing a claim while processing a message.
The client can renew a claim by issuing a ``PATCH`` command to a
specific claim resource and including a new TTL for the claim
(which can be different from the original TTL).
The server resets the age of the claim and applies the new TTL.

The following table shows the possible response codes for this operation:

+--------------------------+-------------------------+-------------------------+
|Response Code             |Name                     |Description              |
+==========================+=========================+=========================+
|200                       |OK                       |The request used invalid |
|                          |                         |URI parameters.          |
+--------------------------+-------------------------+-------------------------+
|204                       |No content               |Success.                 |
+--------------------------+-------------------------+-------------------------+
|400                       |Bad request              |The request included a   |
|                          |                         |non-JSON request body.   |
+--------------------------+-------------------------+-------------------------+
|400                       |Bad request              |The request included     |
|                          |                         |invalid JSON in the      |
|                          |                         |request body.            |
+--------------------------+-------------------------+-------------------------+
|400                       |Bad request              |The request included no  |
|                          |                         |request body.            |
+--------------------------+-------------------------+-------------------------+
|400                       |Bad request              |The request was missing  |
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
|{claimId}    |String |The claim ID.                                               |
+-------------+-------+------------------------------------------------------------+

**Example Update claim: JSON request**

.. code::

   PATCH /v1/queues/demoqueue/claims/51db7067821e727dc24df754 HTTP/1.1
   Host: ord.queues.api.rackspacecloud.com
   Content-type: application/json
   X-Auth-Token: 0f6e9f63600142f0a970911583522217
   Client-ID: e58668fc-26eb-11e3-8270-5b3128d43830
   Accept: application/json
   X-Project-Id: 806067

.. code::

   {
     "ttl": 300,
     "grace": 300
   }


Response
--------

**Example Update claim: JSON response**

.. code::

   HTTP/1.1 204 No Content
