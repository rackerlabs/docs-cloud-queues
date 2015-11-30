.. _gs-delete-queue:

Delete queue
~~~~~~~~~~~~
The delete queue operation immediately deletes a queue and all
of its existing messages.

Following is the operation template:

.. code::

     DELETE {endpoint}/queues/{queue_name}

Following are examples of a delete queue request and response:

**cURL delete queue request**

.. code:: bash

     curl -i -X DELETE https://ord.queues.api.rackspacecloud.com/v1/queues/samplequeue \
     -H "Content-type: application/json" \
     -H "X-Auth-Token: your_auth_token" \
     -H "Accept: application/json" \
     -H "X-Project-Id: your_project_ID"

**Delete queue response**

.. code:: json

     HTTP/1.1 204 No Content
