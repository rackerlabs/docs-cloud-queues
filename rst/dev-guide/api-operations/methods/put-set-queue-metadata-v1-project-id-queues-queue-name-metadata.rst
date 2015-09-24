.. _set-queue-metadata:

^^^^^^^^^^^^^^^^^^
Set queue metadata
^^^^^^^^^^^^^^^^^^
.. code::

    PUT /v1/{project_id}/queues/{queue_name}/metadata

This operation sets metadata for the specified queue.

This operation replaces any existing metadata document in its
entirety. Ensure that you do not accidentally overwrite existing
metadata that you want to retain.

The request body has a limit of 256 KB, including whitespace
(when re-serialized as JSON).

The body of the request includes contextual information about the
way a particular application interacts with the queue. The document
must be valid JSON (Cloud Queues validates it).

The following table shows the possible response codes for this operation:

+--------------------------+-------------------------+-------------------------+
|Response Code             |Name                     |Description              |
+==========================+=========================+=========================+
|204                       |No content               |Success.                 |
+--------------------------+-------------------------+-------------------------+
|400                       |Bad request              |The request body is      |
|                          |                         |empty.                   |
+--------------------------+-------------------------+-------------------------+
|400                       |Bad request              |The request body is      |
|                          |                         |greater than 64 KB.      |
+--------------------------+-------------------------+-------------------------+
|400                       |Bad request              |The request body is not  |
|                          |                         |JSON.                    |
+--------------------------+-------------------------+-------------------------+
|400                       |Bad request              |The request has a UTF-16 |
|                          |                         |char JSON body.          |
+--------------------------+-------------------------+-------------------------+
|400                       |Bad request              |The request has          |
|                          |                         |malformed JSON.          |
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

**Example Set queue metadata: JSON request**

.. code::

   PUT /v1/queues/demoqueue/metadata HTTP/1.1
   Host: ord.queues.api.rackspacecloud.com
   Content-type: application/json
   X-Auth-Token: 0f6e9f63600142f0a970911583522217
   Accept: application/json
   X-Project-Id: 806067

.. code::

   {
      "new metadata":"Omega"
   }

Response
""""""""
**Example Set queue metadata: JSON response**

.. code::

   HTTP/1.1 204 No Content
   Location: /v1/queues/demoqueue/metadata
