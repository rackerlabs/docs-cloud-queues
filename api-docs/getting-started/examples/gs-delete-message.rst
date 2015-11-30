.. _gs-delete-message:

Deleting messages
~~~~~~~~~~~~~~~~~~~

The delete message operation deletes messages that have been processed by a worker.

Following is the operation template:

.. code::

     DELETE {endpoint}/queues/{queue_name}/messages/{message_id}{?claim_id}

The ``message_id`` parameter specifies the message to delete.

The ``claim_id`` parameter specifies that the message is deleted only if
it has the specified claim ID and that claim has not expired. This
specification is useful for ensuring that only one worker processes
any given message. 

When a worker's claim expires before it deletes a
message that it has processed, the worker must roll back any actions
it took based on that message because another worker can now claim
and process the same message.

Following are examples of a delete message request and response:

**cURL delete message request**

.. code:: bash

     curl -i -X DELETE $API_ENDPOINT/queues/samplequeue/messages/51ca00a0c508f154c912b85c?claim_id=51ca011c821e7250f344efd6 \
     -H "Content-type: application/json" \
     -H "X-Auth-Token: $AUTH_TOKEN" \
     -H "Client-ID: e58668fc-26eb-11e3-8270-5b3128d43830" \
     -H "Accept: application/json" \
     -H "X-Project-Id: $TENANT_ID"

**Delete message response**

.. code:: json

     HTTP/1.1 204 No Content
