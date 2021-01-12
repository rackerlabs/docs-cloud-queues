.. _concepts:

==================
|service| Concepts
==================

To use the Cloud Queues API effectively, you should understand the key
concepts described in this section.

How Cloud Queues works
~~~~~~~~~~~~~~~~~~~~~~

Following is an overview of |product name| works:

1. Create a queue to which producers or publishers post messages.

2. Workers (consumers or subscribers) claim or get a message from the
   queue, complete the work in that message, and delete the message.

   If a worker will be offline before it completes the work in a
   message, the worker can retire the claim's time to live (TTL),
   putting the message back into the queue for another worker to claim.

3. Subscribers monitor the claims from these queues to track activity
   and help troubleshoot errors.

For the majority of use cases, |product name| is not responsible for the
ordering of messages. However, if there is only a single producer,
|product name| ensures that messages are handled in a First In, First Out
(FIFO) order.

.. _messaging-patterns:

Messaging patterns
~~~~~~~~~~~~~~~~~~

Cloud Queues supports a variety of messaging patterns including the
following:

* producer-consumer

* publish-subscribe


Producer-consumer
-----------------

The producer-consumer pattern has the following characteristics:

* A producer is programmed to send messages to a queue.
* Multiple workers (or consumers) are programmed to monitor a queue.
* Only one worker can claim a message so that no other worker can claim
  the message and duplicate the work.
* The worker must delete the message when work is done.
* TTL restores a message to an unclaimed state if the worker never
  finishes.

This pattern is ideal for dispatching jobs to multiple processors.

Publish-subscribe
-----------------

Characteristics of the publish-subscribe pattern are:

* The publisher sends a message to a queue.
* All workers (or subscribers) listen to the messages in the queue.
* Multiple workers can take action on a message.
* Workers can send a marker or cursor to skip messages already seen.
* TTL eventually deletes messages.

This pattern is ideal for notification of events to multiple workers at
once.


Use cases
~~~~~~~~~

Queuing systems are used to coordinate tasks within an application. Here
are some examples:

* **Backup**: A backup application might use a queuing system to
  connect the actions that users do in the a control panel to the
  customer's backup agent on a server. When a customer wants to start a
  backup, they simply choose "start backup" on a panel. Doing so causes
  the producer to put a "startBackup" message into the queue. Every few
  minutes, the agent on the customers server (the worker) checks the
  queue to see if it has any new messages to act on. The agent claims
  the "startBackup" message and kicks off the backup on the customer's
  server.

* **Storage**: Gathering statistics for a large, distributed storage
  system can be a long process. The storage system can use a queuing
  system to ensure that jobs complete, even if one initially fails.
  Since messages are not deleted until after the worker has completed
  the job, the storage system can make sure that no job goes undone. If
  the worker fails to complete the job, the message stays in the queue
  to be completed by another server. In this case, a worker claims a
  message to perform a statistics job, but the claim's TTL expired and
  the message is put back into the queue when the job took too long to
  complete (meaning that it most likely failed). By giving the claim a
  TTL, applications can protect themselves from workers going offline
  while processing a message. After a claim's TTL expires, the message
  is put back into the queue for another worker to claim.

* **Email**: The team for an email application is constantly migrating
  customer email from old versions to newer ones, so they develop a
  tool to let customers do it themselves. The migrations take a long
  time, so they cannot be done with single API calls, or by a single
  server. When a user starts a migration job from their portal, the
  migration tool sends messages to the queue with details of how to run
  the migration. A set of migration engines, the consumers in this
  case, periodically check the queues for new migration tasks, claim
  the messages, perform the migration, and update a database with the
  migration details. This process allows a set of servers to work
  together to accomplish large migrations in a timely manner.

Following are some generic use cases for |product name|:

* Distribute tasks among multiple workers (transactional job queues)
* Forward events to data collectors (transactional event queues)
* Publish events to any number of subscribers (publish-subscribe)
* Send commands to one or more agents (point-to-point or
  publish-subscribe)
* Request an action or get information from a Remote Procedure Call
  (RPC) agent
