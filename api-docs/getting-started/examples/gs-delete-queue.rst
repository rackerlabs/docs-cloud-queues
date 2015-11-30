.. _gs-delete-queue:

Deleting a queue
~~~~~~~~~~~~~~~~~~~

The delete queue operation immediately deletes a queue and all
of its existing messages.

Following is the operation template:

.. code::

     DELETE {endpoint}/queues/{queue_name}

Following are examples of a delete queue request and response:

**cURL delete queue request**

.. code:: bash

     curl -i -X DELETE $API_ENDPOINT/queues/samplequeue \
     -H "Content-type: application/json" \
     -H "X-Auth-Token: $AUTH_TOKEN" \
     -H "Accept: application/json" \
     -H "X-Project-Id: $TENANT_ID"

**Delete queue response**

.. code:: json

     HTTP/1.1 204 No Content
