.. _limits:

======
Limits
======

All accounts, by default, have a preconfigured set of thresholds, or *limits*,
to manage capacity and prevent abuse of the system. The system recognizes two
kinds of limits: *rate limits* and *absolute limits*. Rate limits are
thresholds that are reset after a certain amount of time passes. Absolute
limits are fixed. Rate limits are processed via the `Repose service`_.

.. note::

    If the default limits are too low for your particular application,
    contact Rackspace Cloud support to request an increase. All requests
    require reasonable justification.

.. _Repose service: http://www.openrepose.org

Rate limits
~~~~~~~~~~~

Rate limits are thresholds that control the frequency at which the
user can issue specificAPI requests.
Limits are reset after a certain amount of time passes.

With |product name|, you can send over 25 million requests a day per
project ID (approximately 300 requests per second).

If your application slightly exceeds the rate limit, the |product name|
service throttles your requests. The requests will take longer to
perform and will have more latency. If your application greatly exceeds
the 300 request per second rate limit, the API returns the HTTP response
code 429 Too Many Requests. If this occurs, reduce the application's
request rate to the |apiservice| by pausing slightly between each
request. If your application continues to hit this limit and you cannot
slow down the request rate, please contact Rackspace Cloud support.

Absolute limits
~~~~~~~~~~~~~~~

Absolute limits are fixed. Absolute limits control the total
number of specific objects that the user can possess simultaneously.

The following table provides details about the absolute limits for the
|apiservice|.

**Absolute limits**

+--------------+------------------------------------------------------------+
| Type         | Description                        | Limit                 |
+==============+====================================+=======================+
| Limits on    | Number of queue records per page   | 1 - 1000              |
| messages and | of results when listing queues     |                       |
| queues per   +------------------------------------+-----------------------+
| request      | Number of messages per page        | 1 - 2                 |
|              | of results when listing messages   |                       |
|              +------------------------------------+-----------------------+
|              | Number of messages that can be     | 1 - 25                |
|              | posted in a single request         |                       |
|              +------------------------------------+-----------------------+
|              | Number of messages that can be     | 1 - 100               |
|              | claimed at one time                |                       |
|              +------------------------------------+-----------------------+
|              | Number of messages that can be     | 1 - 25                |
|              | deleted in a single bulk delete    |                       |
|              | request                            |                       |
|              +------------------------------------+-----------------------+
|              | Number of messages that can be     | 1 - 25                |
|              | deleted in a get by ID request     |                       |
+--------------+------------------------------------+-----------------------+
| Time limits  | Valid range for a message TTL      | 60 - 1209600          |
|              |                                    | (1 minute to 14 days) |
|              |                                    | 14 days)              |
|              +------------------------------------+-----------------------+
|              | Valid range for a claim TTL        | 60 - 43200 seconds    |
|              |                                    | (1 minute to 12 hours)|
|              +------------------------------------+-----------------------+
|              | Valid range for a claim grace      | 60 - 43200 seconds    |
|              | period                             | (1 minute to 12 hours)|
+--------------+------------------------------------+-----------------------+
| Data limits  | Queue metadata JSON                | Cannot exceed 262144  |
|              |                                    | bytes, including      |
|              |                                    | whitespace (256 KB)   |
|              +------------------------------------+-----------------------+
|              | Message body JSON                  | Cannot exceed 262144  |
|              |                                    | bytes, including      |
|              |                                    | whitespace (256 KB)   |
+--------------+------------------------------------+-----------------------+


.. note::
   For the 256 KB data limit for the message body JSON, if multiple
   messages are included in the request, this limit also applies to the sum
   of the message bodies added together. For example, you may have one
   message body of 256 KB, or up to 10 messages for which the sum of the
   message bodies is 256 KB. A 400 error is triggered if a single message
   body or the sum of multiple message bodies exceed 256 KB in a single
   request.
