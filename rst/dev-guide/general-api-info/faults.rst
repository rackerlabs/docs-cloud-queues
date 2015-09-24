.. _faults:

Faults
~~~~~~
If any Cloud Queues request results in an error, the queuing service
returns an appropriate 4xx or 5xx HTTP status code, and the following
information in the body:

* Title
* Description
* Internal code
* Link to more information

Following is an example of an error message:

.. code::

    HTTP/1.1 400 Bad Request
    Content-Type: application/json

.. code::

    {
       "title":"Unsupported limit",
       "description":"The given limit cannot be negative, and cannot be greater than 50.",
       "code":1092,
       "link":{
          "rel":"help",
          "href":"http://docs.example.com/messages#limit",
          "text":"API documentation for the limit parameter"
       }
    }

Error information for each operation is included in the API operations reference.
