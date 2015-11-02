.. _service-access-endpoints:

~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Service access and endpoints
~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The Cloud Queues service is a regionalized service that allows
customers to select the
regional endpoint where the Cloud Queues service is provisioned.

.. tip::
     To help you decide which regionalized endpoint to use, see the
     considerations for choosing a data center in the
     :kc-article:`About regions <about-regions>` Rackspace Knowledge
     Center article.

**Regionalized service endpoints**

+------------------------+-----------------------------------------------------+
| Region                 | Endpoint                                            |
+========================+=====================================================+
| Chicago (ORD)          | https://ord.queues.api.rackspacecloud.com/v1/       |
|                        +-----------------------------------------------------+
|                        | https://snet-ord.queues.api.rackspacecloud.com/v1/  |
+------------------------+-----------------------------------------------------+
| Dallas/Ft. Worth (DFW) | https://dfw.queues.api.rackspacecloud.com/v1/       |
|                        +-----------------------------------------------------+
|                        | https://snet-dfw.queues.api.rackspacecloud.com/v1/  |
+------------------------+-----------------------------------------------------+
| Hong Kong (HKG)        | https://hkg.queues.api.rackspacecloud.com/v1/       |
|                        +-----------------------------------------------------+
|                        | https://snet-hkg.queues.api.rackspacecloud.com/v1/  |
+------------------------+-----------------------------------------------------+
| London (LON)           | https://lon.queues.api.rackspacecloud.com/v1/       |
|                        +-----------------------------------------------------+
|                        | https://snet-lon.queues.api.rackspacecloud.com/v1/  |
+------------------------+-----------------------------------------------------+
| Northern Virginia (IAD)| https://iad.queues.api.rackspacecloud.com/v1/       |
|                        +-----------------------------------------------------+
|                        | https://snet-iad.queues.api.rackspacecloud.com/v1/  |
+------------------------+-----------------------------------------------------+
| Sydney (SYD)           | https://syd.queues.api.rackspacecloud.com/v1/       |
|                        +-----------------------------------------------------+
|                        | https://snet-syd.queues.api.rackspacecloud.com/v1/  |
+------------------------+-----------------------------------------------------+

If you are working with cloud servers that are in one of the
Rackspace data centers, using the ServiceNet endpoint in the same
data center has no network costs and provides a faster connection.
ServiceNet endpoints are prefixed with ``snet`` in the "Regionalized service
endpoints" table above. ServiceNet is the data center internet network.
In your authentication response (see :ref:`authentication`),
it is listed as InternalURL.

If you are working with servers that are not in one of the
Rackspace data centers, you must use a public endpoint to connect.
In your authentication response, public endpoints are listed as publicURL.
If you are working with servers in multiple data centers or have a
mixed environment where you have servers in your data centers and in
Rackspace data centers, use a public endpoint because it is accessible
from all the servers in the different environments.

.. note::
   You should copy the base URLs directly from the catalog rather than
   trying to construct them manually.

   Rackspace Cloud Identity returns an endpoint with your account ID.
   Note the following information about account ID:

   * Account ID from Cloud Identity is the same as the Project ID given
     by the ``X-Project-ID`` header set. (You might also see account ID
     or project ID referred to as tenant ID.)
   * You do not have to provide the account ID for the Cloud Queues
     API if you have the ``X-Project-ID`` header set. (In this case, the Cloud
     Queues API works with or without the accout ID specified.)
   * Without the ``X-Project-ID`` header, you receive an auth error if
     the account ID is not in the URL.
   * If the account ID is in the URL, the Cloud Queues API will use
     that ID in place of the ``X-Project-ID`` header.
   * Account ID and Project ID refer to your Rackspace account number.

.. tip::
   If you do not know your account ID or which data center you are
   working in, you can find that information in the
   :mycloud:`Cloud Control Panel <>`.
