.. _role-based-access-control:

~~~~~~~~~~~~~~~~~~~~~~~~~
Role Based Access Control
~~~~~~~~~~~~~~~~~~~~~~~~~
Role Based Access Control (RBAC) restricts access to the capabilities of
Rackspace Cloud services, including the Cloud Queues API, to authorized
users only. RBAC enables Rackspace Cloud customers to specify which
account users of their Cloud account have access to which Cloud Queues
API service capabilities, based on
:ref:`roles defined by Rackspace <rbac-roles-available>`.
The permissions to perform certain operations in Cloud Queues
API – create, read, update, delete –
are assigned to specific roles, and these roles can be assigned by the
Cloud account admin user to account users of the account.


.. _rbac-assign-roles:

Assigning roles to account users
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The account owner (identity:user-admin) can create account users on the
account and then assign roles to those users. The roles grant the
account users specific permissions for accessing the capabilities of the
Cloud Queues service. Each account has only one account owner, and that
role is assigned by default to any Rackspace Cloud account when the
account is created.

See the :rax-devguide:`Cloud Identity Client Developer Guide
<cloud-identity/v2>` for
information on how to perform these tasks:

* Create account users
* Assign roles to account users
* Delete roles from account users

..  note::
	  The account admin user (identity:user-admin) role cannot hold any
		additional roles because it already has full access to all capabilities
		by default.


.. _rbac-roles-available:

Roles available for Cloud Queues
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Three roles (admin, creator, and observer) can be used to access the
Cloud Queues API specifically. The following table describes these
roles and their permissions:

**Cloud Queues product roles and capabilities**

+--------------------------------------+--------------------------------------+
| Role name                            | Role permissions                     |
+======================================+======================================+
| admin                                | Provides Create, Read,               |
|                                      | Update, and Delete permissions in    |
|                                      | Cloud Queues, where access is        |
|                                      | granted.                             |
+--------------------------------------+--------------------------------------+
| creator                              | Provides Create, Read and            |
|                                      | Update permissions in Cloud Queues,  |
|                                      | where access is granted.             |
+--------------------------------------+--------------------------------------+
| observer                             | Provides Read permission             |
|                                      | in Cloud Queues, where access is     |
|                                      | granted.                             |
+--------------------------------------+--------------------------------------+

Additionally, two multi-product roles apply to all products. Users with
multi-product roles inherit access to future products when those products
become RBAC-enabled. The following table describes these roles and
their permissions:

**Multi-product (global) roles and permissions**

+--------------------------------------+--------------------------------------+
| Role name                            | Role permissions                     |
+======================================+======================================+
| admin                                | Provides Create, Read,               |
|                                      | Update, and Delete permissions in    |
|                                      | all products, where access is        |
|                                      | granted.                             |
+--------------------------------------+--------------------------------------+
| observer                             | Provides Read permission             |
|                                      | in all products, where access is     |
|                                      | granted.                             |
+--------------------------------------+--------------------------------------+

.. _rbac-resolve-conflicts:

Resolving conflicts between RBAC multi-product vs. custom (product-specific) roles
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The account owner can set roles for both multi-product and Cloud Queues
scope, and it is important to understand how any potential conflicts
among these roles are resolved. When two roles appear to conflict, the
role that provides the more extensive permissions takes precedence.
Therefore, admin roles take precedence over observer and creator roles,
because admin roles provide more permissions.

The following table shows two examples of how potential conflicts
between user roles in the Control Panel are resolved:

+----------------------------------+-----------------------+-----------------------------+
| Permission configuration         | View of Permission    | Can the user perform        |
|                                  | in the Control Panel  | product admin functions     |
|                                  |                       | in the Control Panel?       |
+==================================+=======================+=============================+
| User is assigned the following   | Appears that the user | Yes, Cloud Queues           |
| roles: multi-product **observer**| has only the          | only. The user has          |
| and Cloud Queues                 | multi-product         | **observer** role for the   |
| **admin**                        | **observer** role     | rest of the products.       |
+----------------------------------+-----------------------+-----------------------------+
| User is assigned the following   | Appears that the user | Yes, for all products.      |
| roles: multi-product             | has only the          | The Cloud Queues            |
| **admin** and Cloud Queues       | multi-product         | **observer** role is        |
| **observer**                     | **admin** role.       | ignored.                    |
+----------------------------------+-----------------------+-----------------------------+

.. _rbac-permissions-matrix:

RBAC permissions cross-reference to Cloud Queues API operations
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
API operations for Cloud Queues are accessible to users based on user
role assignment. For information about which roles are available to
which users, review the
:kc-article:`Permissions Matrix for Role-Based Access Control
<permissions-matrix-for-role-based-access-control-rbac>`.
