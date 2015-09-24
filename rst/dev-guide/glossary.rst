.. _glossary:

Glossary
--------

Claim
	The process of a worker checking out a message to perform a task.
	Claiming a message prevents other workers from attempting to process
	the same messages.

Claim TTL
	Defines how long a message will be in claimed state. A message can
	be claimed by one worker at a time.

Consumer
	A server that claims messages from the queue.

Message
	A task, a notification, or any meaningful data that a producer or
	publisher sends to the queue. A message exists until it is deleted
	by a recipient or automatically by the system based on a TTL
	(time-to-live) value.

Message TTL
	Defines how long a message will be accessible.

Producer
	A server or application that sends messages to the queue.

Producer - Consumer
	A pattern where each worker application that reads the queue has to
	claim the message in order to prevent duplicate processing. Later,
	when work is done, the worker is responsible for deleting the
	message. If message is not deleted in a predefined time, it can be
	claimed by other workers.

Publisher
	A server or application that posts messages to the queue with the
	intent to distribute information or updates to multiple subscribers.

Publisher - Subscriber
	A pattern where all worker applications have access to all messages
	in the queue. Workers cannot delete or update messages.

Queue
	The entity that holds messages. Ideally, a queue is created per work
	type. For example, if you want to compress files, you would create a
	queue dedicated to this job. Any application that reads from this
	queue would only compress files.

Subscriber
	An observer that watches messages like an RSS feed but does not
	claim any messages.

TTL
	Time-to-live value.

Worker
	A client that claims messages from the queue and performs actions
	based on those messages.
