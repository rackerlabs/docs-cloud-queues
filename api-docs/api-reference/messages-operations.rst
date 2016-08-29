.. _messages-operations:

========
Messages
========

This section describes message operations that are supported by the
|apiservice|.

.. note::
   All message-related operations require that Client-ID be included in the
   headers. This is to ensure that messages are not echoed back to the
   client that posted them unless the client explicitly requests this.

.. include:: methods/post-post-message-v1-project-id-queues-queue-name-messages.rst
.. include:: methods/get-get-messages-v1-project-id-queues-queue-name-messages.rst
.. include:: methods/get-get-messages-by-id-v1-project-id-queues-queue-name-messages.rst
.. include:: methods/delete-bulk-delete-messages-by-id-v1-project-id-queues-queue-name-messages.rst
.. include:: methods/get-show-message-details-v1-project-id-queues-queue-name-messages-messageid.rst
.. include:: methods/delete-delete-message-v1-project-id-queues-queue-name-messages-messageid.rst
