
.. THIS OUTPUT IS GENERATED FROM THE WADL. DO NOT EDIT.

Check Queue Existence
~~~~~~~~~~~~~~~~~~~~~~~~~

.. code::

    GET /v1/{project_id}/queues/{queue_name}

Verifies whether the specified queue 				exists.

This operation verifies whether the specified queue 				exists.

You can also use ``HEAD`` instead of ``GET`` for the 				verb.



This table shows the possible response codes for this operation:


+--------------------------+-------------------------+-------------------------+
|Response Code             |Name                     |Description              |
+==========================+=========================+=========================+
|204                       |OK                       |The requested queue      |
|                          |                         |exists.                  |
+--------------------------+-------------------------+-------------------------+
|404                       |Not found                |The requested queue does |
|                          |                         |not exist.               |
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








**Example Check Queue Existence: JSON request**


.. code::

    GET /v1/queues/demoqueue HTTP/1.1
    Host: ord.queues.api.rackspacecloud.com
    X-Project-Id: 806067


Response
^^^^^^^^^^^^^^^^^^





**Example Check Queue Existence: JSON response**


.. code::

    HTTP/1.0 204 OK

