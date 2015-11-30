.. _gs-release-claim:

Releasing a claim
~~~~~~~~~~~~~~~~~~~

The release claim operation immediately releases all messages associated with a specified 
claim ID. This action makes all remaining, undeleted messages associated with the claim 
available to be processed by other workers.

Following is the operation template:

.. code::

     DELETE {endpoint}/queues/{queue_name}/claims/{claim_id}

This operation is useful when a worker is performing a graceful
shutdown, fails to process one or more messages, or is taking
longer than expected to process messages and wants to make the
remainder of the messages available to other workers.

Following are examples of a release claim request and response:

**cURL relesase claim request**

.. code:: bash

     curl -i -X DELETE $API_ENDPOINT/queues/samplequeue/claims/51ca011c821e7250f344efd6 \
     -H "Content-type: application/json" \
     -H "X-Auth-Token: $AUTH_TOKEN" \
     -H "Client-ID: e58668fc-26eb-11e3-8270-5b3128d43830"  \
     -H "Accept: application/json" \
     -H "X-Project-Id: $TENANT_ID"

**Release claim response**

.. code:: json

     HTTP/1.1 204 No Content
