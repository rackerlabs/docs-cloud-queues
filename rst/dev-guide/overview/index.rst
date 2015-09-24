.. _overview:

-------------
About the API
-------------
Rackspace Cloud Queues is an open source, scalable, and highly available
message and notifications service. Cloud Queues supports a variety of
messaging patterns. Users of this service can create and manage a
`producer-consumer <producer_consumer.html>`__ or a
`publish-subscriber <publish_subscribe.html>`__ model from one simple
API. Unlimited queues and messages give Cloud Queues users the
flexibility they need to create powerful web applications in the cloud.

Cloud Queues is based on the OpenStack Marconi project.

Cloud Queues consists of a few basic components: queues, messages,
claims, and statistics. In the producer-consumer model, users create
queues in which producers, or servers, can post messages. Workers, or
consumers, can then claim those messages and delete them after they
complete the actions associated with the messages. A single claim can
contain multiple messages, and administrators can query claims for
status.

In the publisher-subscriber model, messages are posted to a queue as in
the producer-consumer model, but messages are never claimed. Instead,
subscribers, or watchers, send **GET** requests to pull all messages
that have been posted since their last request. In this model, a message
remains in the queue, unclaimed, until the message's time to live (TTL)
has expired.

In both of these models, administrators can get queue statistics that
display the most recent and oldest messages, the number of unclaimed
messages, and more.

.. toctree:: :hidden:
   :maxdepth: 3

   additional-resources
   contract-changes
   pricing-service-level
