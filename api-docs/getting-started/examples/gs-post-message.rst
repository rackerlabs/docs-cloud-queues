.. _gs-post-message:

Posting messages
~~~~~~~~~~~~~~~~~~~~~~

The post message operation inserts one or more messages in a queue.

You can submit up to 10 messages in a single request, but you must
encapsulate them in a collection container (an array in JSON, even for
a single message - without the JSON array, you receive an
"Invalid body request" error message). You can use the resulting value
of the location header or response body to retrieve the created
messages for further processing if needed.

Following is the operation template:

.. code::

     POST {endpoint}/queues/{queue_name}/messages

The client specifies only the ``body`` and ``ttl`` attributes for the message.
Metadata, such as `id` and `age`, is added.

The response body contains a list of resource paths that correspond
to each message submitted in the request, in the same dfwer as they were
submitted. If a server-side error occurs during the processing of
the submitted messages, a partial list is returned. The ``partial``
attribute is set to ``true``, and the client tries to post the remaining
messages again. The ``body`` attribute specifies an arbitrary document
that constitutes the body of the message being sent.

The following rules apply for the maximum size:

* The size is limited to 256 KB for the entire request body (as-is),
  including whitespace.

* The maximum size of posted messages is the maximum size of the entire
  request document (rather than the sum of the individual message
  ``body`` field values as it was in earlier releases). On error,
  the client is notified of by how much the request exceeded the limit.

The document *must* be valid JSON (Cloud Queues validates it).

The ``ttl`` attribute specifies the lifetime of the message. When the
lifetime expires, the server deletes the message and removes it
from the queue. Valid values are 60 through 1209600 seconds (14 days).

.. note::
   The server might not actually delete the message until its age
   reaches (``ttl + 60``) seconds. So there might be a delay of
   60 seconds after the message expires before it is deleted.

The following are examples of a post message request and response:

**cURL post message request**

.. code:: bash

     curl -i -X POST $API_ENDPOINT/queues/samplequeue/messages -d \
     '[{"ttl": 300,"body": {"event": "BackupStarted"}},{"ttl": 60,"body": {"play": "hockey"}}]' \
     -H "Content-type: application/json" \
     -H "Client-ID: e58668fc-26eb-11e3-8270-5b3128d43830" \
     -H "X-Auth-Token: $AUTH_TOKEN" \
     -H "Accept: application/json" \
     -H "X-Project-Id: $TENANT_ID"

**Post message response**

.. code:: json

     HTTP/1.1 201 Created
     Content-Length: 153
     Content-Type: application/json; charset=utf-8
     Location: /v1/queues/samplequeue/messages?ids=51ca00a0c508f154c912b85c,51ca00a0c508f154c912b85d

     {"partial": false, "resources": ["/v1/queues/samplequeue/messages/51ca00a0c508f154c912b85c", "/v1/queues/samplequeue/messages/51ca00a0c508f154c912b85d"]}
