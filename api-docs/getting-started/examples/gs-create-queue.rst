.. _gs-create-queue:

Creating a queue
~~~~~~~~~~~~~~~~~~

The queue operation creates a queue in the region of your choice.

The body of the PUT request is empty.

Following is the operation template:

.. code::

     PUT {endpoint}/queues/{queue_name}

The `queue_name` parameter specifies the name to give the queue. The name
*must not* exceed 64 bytes in length and is limited to US-ASCII letters,
digits, underscores, and hyphens.

Following are examples of a create queue request and response:

**cURL create queue request**

.. code:: bash

     curl -i -X PUT $API_ENDPOINT/queues/samplequeue \
     -H "X-Auth-Token: $AUTH_TOKEN" \
     -H "Accept: application/json" \
     -H "X-Project-Id: $TENANT_ID"

**Create queue response**

.. code:: json

     HTTP/1.1 201 Created
     Content-Length: 0
     Location: /v1/queues/samplequeue
