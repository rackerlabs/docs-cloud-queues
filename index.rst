.. _index:

===============================================
Rackspace |product name| API |contract version|
===============================================

*Last updated:* |today|

The Rackspace |product name| service  is an open source, scalable, and highly
available message and notifications service based on the OpenStack Marconi
project. It supports a variety of messaging patterns and enables customers to
create and manage a producer-consumer or a publish-subscriber model
(:ref:`messaging-patterns`) from one simple API. Unlimited queues and messages
give |product name| users the flexibility they need to create powerful web
applications in the cloud.

This guide is intended to assist software developers who want to develop
applications by using the REST application programming interface (API) for
the |product name| service.

To use the information provided here, you should have a general understanding
of the service and have access to an installation of it. You should also be
familiar with the following technologies:

* RESTful web services
* HTTP/1.1
* JSON or XML serialization formats

Use the following links to jump directly to user and reference information for
the |product name| service REST API:

- :ref:`Getting started <getting-started-guide>`
- :ref:`General API information <general-api-info>`
- :ref:`API reference <api-reference>`
- :ref:`Release notes <release-notes-collection>`

.. note::

   You can also use |product name| from the Cloud Control Panel.

|service| consists of a few basic components: queues, messages,
claims, and statistics.

In the producer-consumer model, users create
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

    Cloud Queues 1.0 <self>
    getting-started/index
    general-api-info/index
    api-reference/index
    release-notes/index
    service-updates
    additional-resources
    copyright
