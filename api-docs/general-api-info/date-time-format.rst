.. _date--time-format:

~~~~~~~~~~~~~~~~~~~~
Date and time format
~~~~~~~~~~~~~~~~~~~~
For the display and consumption of date and time values, the Cloud
Queues service uses a date format that complies with ISO 8601:

.. code::

    yyyy-MM-dd'T'HH:mm:ss.SSSZ

For example, May 19, 2013 at 8:07:08 A.M., GMT-5 would have the
following format:

.. code::

    2013-05-19T08:07:08-05:00

The following table specifies the date and time format codes and descriptions:

+------+-----------------------------------------------------------+
| Code | Description                                               |
+======+===========================================================+
| yyyy | Four digit year                                           |
+------+-----------------------------------------------------------+
| MM   | Two digit month                                           |
+------+-----------------------------------------------------------+
| DD   | Two digit day                                             |
+------+-----------------------------------------------------------+
| T    | Separator for date/time                                   |
+------+-----------------------------------------------------------+
| HH   | Two digit hour (00-23)                                    |
+------+-----------------------------------------------------------+
| mm   | Two digit minute                                          |
+------+-----------------------------------------------------------+
| ss   | Two digit second                                          |
+------+-----------------------------------------------------------+
| Z    | RFC 8601 timezone (offset from GMT). If Z is not replaced |
|      | with the offset from GMT, it indicates a 00:00 offset.    |
+------+-----------------------------------------------------------+
