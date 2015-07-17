=============================================================================
Query Claim -  Queues
=============================================================================

Query Claim
~~~~~~~~~~~~~~~~~~~~~~~~~

`Request <GET_query_claim_v1_project_id_queues_queue_name_claims_claimid_.rst#request>`__
`Response <GET_query_claim_v1_project_id_queues_queue_name_claims_claimid_.rst#response>`__

.. code-block:: javascript

    GET /v1/{project_id}/queues/{queue_name}/claims/{claimId}

Queries the specified claim for a specified queue.

This operation queries the specified claim for the specified queue. Claims with malformed IDs or claims that are not found by ID are ignored.



This table shows the possible response codes for this operation:


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
|404                       |Not found                |The request included an  |
|                          |                         |expired claim.           |
+--------------------------+-------------------------+-------------------------+
|404                       |Not found                |The request included a   |
|                          |                         |claim from a non-        |
|                          |                         |existing queue.          |
+--------------------------+-------------------------+-------------------------+
|404                       |Not found                |The request included a   |
|                          |                         |non-existing claim ID.   |
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
|{claimId}    |xsd:string |The claim ID.                                               |
+-------------+-----------+------------------------------------------------------------+








**Example Query Claim: JSON request**


.. code::

    GET /v1/queues/demoqueue/claims/51db7067821e727dc24df754 HTTP/1.1
    Host: ord.queues.api.rackspacecloud.com
    Content-type: application/json
    X-Auth-Token: 0f6e9f63600142f0a970911583522217
    Client-ID: e58668fc-26eb-11e3-8270-5b3128d43830
    Accept: application/json
    X-Project-Id: 806067


Response
^^^^^^^^^^^^^^^^^^





**Example Query Claim: JSON request**


.. code::

    HTTP/1.1 200 OK
    Content-Length: 263
    Content-Type: application/json; charset=utf-8
    Content-Location: /v1/queues/demoqueue/claims/51db7067821e727dc24df754

