
.. THIS OUTPUT IS GENERATED FROM THE WADL. DO NOT EDIT.

List Queues
~~~~~~~~~~~~~~~~~~~~~~~~~

.. code::

    GET /v1/{project_id}/queues

Lists queues.

This operation lists queues for the project. The 				queues are sorted alphabetically by name.

A request to list queues when you have no queues in 				your account returns 204, instead of 200, because 				there was no information to send back.



This table shows the possible response codes for this operation:


+--------------------------+-------------------------+-------------------------+
|Response Code             |Name                     |Description              |
+==========================+=========================+=========================+
|200                       |OK                       |Success. The URI might   |
|                          |                         |have an invalid          |
|                          |                         |parameter (something     |
|                          |                         |other than limit,        |
|                          |                         |marker, or detailed),    |
|                          |                         |but the invalid          |
|                          |                         |parameter is ignored.    |
+--------------------------+-------------------------+-------------------------+
|204                       |No content               |You have no queues in    |
|                          |                         |your account, or the     |
|                          |                         |request has a non-       |
|                          |                         |existing value for       |
|                          |                         |marker.                  |
+--------------------------+-------------------------+-------------------------+
|400                       |Bad request              |The request has a        |
|                          |                         |negative or zero value   |
|                          |                         |for the limit, a non-    |
|                          |                         |boolean value for        |
|                          |                         |detailed, or a header    |
|                          |                         |that has missing fields. |
+--------------------------+-------------------------+-------------------------+
|401                       |Unauthorized             |The request header has   |
|                          |                         |an invalid auth token.   |
+--------------------------+-------------------------+-------------------------+
|404                       |Not found                |The requested queue does |
|                          |                         |not exist.               |
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



This table shows the query parameters for the request:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|marker                    |xsd:string *(Required)*  |Specifies the name of    |
|                          |                         |the last queue received  |
|                          |                         |in a previous request,   |
|                          |                         |or none to get the first |
|                          |                         |page of results.         |
+--------------------------+-------------------------+-------------------------+
|limit                     |xsd:integer *(Required)* |Specifies the number of  |
|                          |                         |queues to return. The    |
|                          |                         |default value for the    |
|                          |                         |number of queues         |
|                          |                         |returned is 10. If you   |
|                          |                         |do not specify this      |
|                          |                         |parameter, the default   |
|                          |                         |number of queues is      |
|                          |                         |returned.                |
+--------------------------+-------------------------+-------------------------+
|detailed                  |xsd:boolean *(Required)* |Determines whether queue |
|                          |                         |metadata is included in  |
|                          |                         |the response. The        |
|                          |                         |default value for this   |
|                          |                         |parameter is ``false``,  |
|                          |                         |which excludes the       |
|                          |                         |metadata.                |
+--------------------------+-------------------------+-------------------------+







**Example List Queues: JSON request**


.. code::

    GET /v1/queues HTTP/1.1
    Host: ord.queues.api.rackspacecloud.com
    Content-type: application/json
    X-Auth-Token: 0f6e9f63600142f0a970911583522217
    Accept: application/json
    X-Project-Id: 806067


Response
^^^^^^^^^^^^^^^^^^





**Example List Queues: JSON response**


.. code::

    HTTP/1.1 200 OK
    Content-Length: 3170
    Content-Type: application/json; charset=utf-8
    Content-Location: /v1/queues

