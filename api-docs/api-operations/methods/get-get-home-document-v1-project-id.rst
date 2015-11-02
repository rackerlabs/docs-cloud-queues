.. _get-home-document:

^^^^^^^^^^^^^^^^^
Get home document
^^^^^^^^^^^^^^^^^
.. code::

    GET /v1/{project_id}

This operation gets the home document.

The entire API is discoverable from a single starting point,
the home document. To explore the entire API, you need to know only
this one URI. This document is cacheable.

The home document lets you write clients by using relational links,
so clients do not have to construct their own URLs. You can click
through and view the JSON doc in your browser.

For more information about home documents, see
`http://tools.ietf.org/html/draft-nottingham-json-home-02
<http://tools.ietf.org/html/draft-nottingham-json-home-02>`__.

The following table shows the possible response codes for this operation:

+--------------------------+-------------------------+-------------------------+
|Response Code             |Name                     |Description              |
+==========================+=========================+=========================+
|200                       |OK                       |Success.                 |
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

.. note:: This operation does not accept a request body.

**Example Get home document: JSON request**

.. code::

   GET /v1 HTTP/1.1
   Host: ord.queues.api.rackspacecloud.com

Response
""""""""
**Example Get home document: JSON response**

.. code::

   HTTP/1.0 200 OK
   Cache-Control: max-age=86400
   Content-Length: 4345
   Content-Type: application/json-home
   Date: Tue, 06 Sep 2013 16:31:48 GMT
   Server: WSGIServer/0.1 Python/2.7.3

.. code::

   {
      "resources":{
         "rel/queue":{
            "href-template":"/queues/{queue_name}",
            "href-vars":{
               "queue_name":"param/queue_name"
            },
            "hints":{
               "allow":[
                  "GET",
                  "HEAD",
                  "PUT",
                  "DELETE"
               ],
               "formats":{
                  "application/json":{

                  }
               }
            }
         },
         "rel/queue-metadata":{
            "href-template":"/queues/{queue_name}/metadata",
            "href-vars":{
               "queue_name":"param/queue_name"
            },
            "hints":{
               "allow":[
                  "GET",
                  "PUT"
               ],
               "formats":{
                  "application/json":{

                  }
               }
            }
         },
         "rel/queue-stats":{
            "href-template":"/queues/{queue_name}/stats",
            "href-vars":{
               "queue_name":"param/queue_name"
            },
            "hints":{
               "allow":[
                  "GET"
               ],
               "formats":{
                  "application/json":{

                  }
               }
            }
         },
         "rel/queues":{
            "href-template":"/queues{?marker,limit,detailed}",
            "href-vars":{
               "marker":"param/marker",
               "detailed":"param/detailed",
               "limit":"param/queue_limit"
            },
            "hints":{
               "allow":[
                  "GET"
               ],
               "formats":{
                  "application/json":{

                  }
               }
            }
         },
         "rel/post-messages":{
            "href-template":"/v1/queues/{queue_name}/messages",
            "href-vars":{
               "queue_name":"param/queue_name"
            },
            "hints":{
               "accept-post":[
                  "application/json"
               ],
               "allow":[
                  "POST"
               ],
               "formats":{
                  "application/json":{

                  }
               }
            }
         },
         "rel/messages":{
            "href-template":"/queues/{queue_name}/messages{?marker,limit,echo,include_claimed}",
            "href-vars":{
               "marker":"param/marker",
               "include_claimed":"param/include_claimed",
               "queue_name":"param/queue_name",
               "limit":"param/messages_limit",
               "echo":"param/echo"
            },
            "hints":{
               "allow":[
                  "GET"
               ],
               "formats":{
                  "application/json":{

                  }
               }
            }
         },
         "rel/claim":{
            "href-template":"/v1/queues/{queue_name}/claims{?limit}",
            "href-vars":{
               "queue_name":"param/queue_name",
               "limit":"param/claim_limit"
            },
            "hints":{
               "accept-post":[
                  "application/json"
               ],
               "allow":[
                  "POST"
               ],
               "formats":{
                  "application/json":{

                  }
               }
            }
         }
      }
   }
