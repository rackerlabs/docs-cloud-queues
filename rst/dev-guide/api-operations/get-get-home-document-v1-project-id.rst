
.. THIS OUTPUT IS GENERATED FROM THE WADL. DO NOT EDIT.

Get Home Document
~~~~~~~~~~~~~~~~~~~~~~~~~

.. code::

    GET /v1/{project_id}

Gets the home document.

This operation gets the home document.

The entire API is discoverable from a single 				starting point, the home document. To explore the 				entire API, you need to know only this one URI. This 				document is cacheable.

The home document lets you write clients by using 				relational links, so clients do not have to construct 				their own URLs. You can click through and view the 				JSON doc in your browser.

For more information about home documents, see `http://tools.ietf.org/html/draft-nottingham-json-home-02 <http://tools.ietf.org/html/draft-nottingham-json-home-02>`__.



This table shows the possible response codes for this operation:


+--------------------------+-------------------------+-------------------------+
|Response Code             |Name                     |Description              |
+==========================+=========================+=========================+
|200                       |OK                       |Success.                 |
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








**Example Get Home Document: JSON request**


.. code::

    GET /v1 HTTP/1.1
    Host: ord.queues.api.rackspacecloud.com


Response
^^^^^^^^^^^^^^^^^^





**Example Get Home Document: JSON response**


.. code::

    HTTP/1.0 200 OK
    Cache-Control: max-age=86400
    Content-Length: 4345
    Content-Type: application/json-home
    Date: Tue, 06 Sep 2013 16:31:48 GMT
    Server: WSGIServer/0.1 Python/2.7.3

