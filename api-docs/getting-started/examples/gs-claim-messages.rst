.. _gs-claim-messages:

Claiming messages for processing 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The claim messages operation gets a set of messages from a specified message queue 
(up to the value of the ``limit`` parameter) from oldest to newest and skips any
messages that are already claimed. If there are no messages available
to claim, the Cloud Queues service returns an HTTP `204 No Content`
response code.

Following is the operation template:

.. code::

     POST {endpoint}/queues/{queue_name}/claims{?limit}
     Content-Type: application/json

     {
         "ttl": {claim_ttl},
         "grace": {message_grace}
     }

The client (worker) needs to delete the message when it has finished
processing it. The client deletes the message before the claim expires
to ensure that the message is processed only once. 

If a client needs
more time, Cloud Queues provides the :ref:`update claim<patch-update-claim>` operation 
to make changes.

As part of the delete operation,
workers specify the claim ID (which is best done by simply using
the provided href). If workers perform these actions, then if a claim
simply expires, the server can return an error and notify the worker
of a possible race condition. This action gives the worker a chance to
roll back its own processing of the given message because another
worker can claim the message and process it.

The age given for a claim is relative to the server's clock. The claim's
age is useful for determining how quickly messages are getting processed
and whether a given message's claim is about to expire.

When a claim expires, it is released back to the queue for other
workers to claim. (If the original worker failed to process the message,
another client worker can then claim the message.)

The ``limit`` parameter specifies the number of messages to claim.
If a ``limit`` value is not specified, Cloud Queues claims 10 messages.
After the messages are successfully claimed, Cloud Queues returns
10 messages in the response.

Messages are claimed based on the number of messages *available*. The server
might claim and return less than the requested number of messages.

If you specify a value for the ``limit`` parameter and the value is less than
or equal to 100, Cloud Queues lets you claim free messages up to the
number specified by the ``limit`` parameter. For example, if only 23 messages
are free and ``limit`` is 100, Cloud Queues claims all 23 messages and
returns 23 messages in the response. If 120 free messages are available
and ``limit`` is 100, Cloud Queues claims the oldest 100 messages and returns
100 messages in response.

The ``ttl`` attribute specifies the lifetime of the claim. While messages
are claimed, they are not available to other workers. The value must
be between 60 and 43200 seconds (12 hours).

The ``grace`` attribute specifies the message grace period in seconds. Valid
values are between 60 and 43200 seconds (12 hours). To deal with
workers that have stopped responding (for up to 1209600 seconds or 14
days, including claim lifetime), the server extends the lifetime of
claimed messages to be at least as long as the lifetime of the claim
itself, plus the specified grace period. If a claimed message normally
lives longer than the grace period, its expiration is not adjusted.

Following are examples of a claim messages request and response:

**cURL claim messages request**

.. code:: bash

     curl -i -X POST $API_ENDPOINT/queues/samplequeue/claims -d \
     '{"ttl": 300,"grace":300}' \
     -H "Content-type: application/json" \
     -H "Client-ID: e58668fc-26eb-11e3-8270-5b3128d43830" \
     -H "X-Auth-Token: $AUTH_TOKEN" \
     -H "Accept: application/json" \
     -H "X-Project-Id: $TENANT_ID"

**Claim messages response**

.. code:: json

     HTTP/1.1 201 OK
     Content-Length: 164
     Content-Type: application/json; charset=utf-8
     Location: /v1/queues/samplequeue/claims/51ca011c821e7250f344efd6
     X-Project-Id: ;;;;$TENANT_ID!bold;;;;

     [
       {
         "body": {
           "event": "BackupStarted"
         },
         "age": 124,
         "href": "/v1/queues/samplequeue/messages/51ca00a0c508f154c912b85c?claim_id=51ca011c821e7250f344efd6",
         "ttl": 300
       }
     ]
