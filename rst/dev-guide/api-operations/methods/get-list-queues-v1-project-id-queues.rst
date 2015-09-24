.. _get-list-queues-v1-project-id-queues:

^^^^^^^^^^^
List queues
^^^^^^^^^^^
.. code::

    GET /v1/{project_id}/queues

This operation lists queues for the project. The queues are sorted
alphabetically by name.

A request to list queues when you have no queues in your account returns 204,
instead of 200, because there was no information to send back.

The following table shows the possible response codes for this operation:

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

The following table shows the query parameters for the request:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|marker                    |String *(Optional)*      |Specifies the name of    |
|                          |                         |the last queue received  |
|                          |                         |in a previous request,   |
|                          |                         |or none to get the first |
|                          |                         |page of results.         |
+--------------------------+-------------------------+-------------------------+
|limit                     |Integer *(Optional)*     |Specifies the number of  |
|                          |                         |queues to return. The    |
|                          |                         |default value for the    |
|                          |                         |number of queues         |
|                          |                         |returned is 10. If you   |
|                          |                         |do not specify this      |
|                          |                         |parameter, the default   |
|                          |                         |number of queues is      |
|                          |                         |returned.                |
+--------------------------+-------------------------+-------------------------+
|detailed                  |Boolean *(Optional)*     |Determines whether queue |
|                          |                         |metadata is included in  |
|                          |                         |the response. The        |
|                          |                         |default value for this   |
|                          |                         |parameter is ``false``,  |
|                          |                         |which excludes the       |
|                          |                         |metadata.                |
+--------------------------+-------------------------+-------------------------+

.. note:: This operation does not accept a request body.

**Example List queues: JSON request**

.. code::

   GET /v1/queues HTTP/1.1
   Host: ord.queues.api.rackspacecloud.com
   Content-type: application/json
   X-Auth-Token: 0f6e9f63600142f0a970911583522217
   Accept: application/json
   X-Project-Id: 806067

Response
""""""""
**Example List queues: JSON response**

.. code::

   HTTP/1.1 200 OK
   Content-Length: 3170
   Content-Type: application/json; charset=utf-8
   Content-Location: /v1/queues

.. code::

   {
      "queues":[
         {
            "href":"/v1/queues/036b184b28fcb548349af623079119c6a966cbc",
            "name":"036b184b28fcb548349af623079119c6a966cbc"
         },
         {
            "href":"/v1/queues/0441f28617afbdecf4887e635fd0777fb3cec38",
            "name":"0441f28617afbdecf4887e635fd0777fb3cec38"
         },
         {
            "href":"/v1/queues/0f8f0eff158922874536efa9cf8412b9e0fd07a",
            "name":"0f8f0eff158922874536efa9cf8412b9e0fd07a"
         },
         {
            "href":"/v1/queues/160f981379972a4a0afaee5f5394a5d960c410e",
            "name":"160f981379972a4a0afaee5f5394a5d960c410e"
         },
         {
            "href":"/v1/queues/2888a4527d0a11a3d82202d800f8e90eebd60ea",
            "name":"2888a4527d0a11a3d82202d800f8e90eebd60ea"
         },
         {
            "href":"/v1/queues/2ad8eeca7f53d480d8ca4885d620643bfc6a7f9",
            "name":"2ad8eeca7f53d480d8ca4885d620643bfc6a7f9"
         },
         {
            "href":"/v1/queues/3926ce2051db957d76a04cb2ea2d89fd49e6894",
            "name":"3926ce2051db957d76a04cb2ea2d89fd49e6894"
         },
         {
            "href":"/v1/queues/46b30ebd60186c30194039824e6405300dc0903",
            "name":"46b30ebd60186c30194039824e6405300dc0903"
         },
         {
            "href":"/v1/queues/486d5af3e057ee1a430eee3ee845aeb60c900d3",
            "name":"486d5af3e057ee1a430eee3ee845aeb60c900d3"
         },
         {
            "href":"/v1/queues/58e8622645f07c7673412acbed51abb97ddb25d",
            "name":"58e8622645f07c7673412acbed51abb97ddb25d"
         }
      ],
      "links":[
         {
            "href":"/v1/queues?marker=58e8622645f07c7673412acbed51abb9",
            "rel":"next"
         }
      ]
   }
