
.. _post-add-replica-to-an-ha-instance-version-accountid-ha-haid-action:

Add Replica to an HA instance
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    POST /{version}/{accountId}/ha/{haId}/action

Add a replica node to the HA group specified by {ha_id}.

This operation adds a replica node to the HA group specified by {ha_id}. The HA instance 
goes into the ``ADDING_REPLICA`` state as a result of this action. It switches back to 
``ACTIVE`` once the operation is complete.

.. warning::
   Adding a new replica node would restart the mha manager service (which monitors the 
   source/replica instances to trigger failover) and the haproxy service on the load 
   balancer nodes. Refer to the  article for more details about these components: 
   :how-to:`High Availability for Cloud Databases <high-availability-for-cloud-databases>`.
   
   

The following table lists the required and optional attributes for creating a replica for an HA instance.



This table shows the possible response codes for this operation:


+--------------------------+-------------------------+-------------------------+
|Response Code             |Name                     |Description              |
+==========================+=========================+=========================+
|202                       |Accepted                 |The request has been     |
|                          |                         |accepted for processing. |
+--------------------------+-------------------------+-------------------------+
|400                       |Bad Request              |The request is missing   |
|                          |                         |one or more elements, or |
|                          |                         |the values of some       |
|                          |                         |elements are invalid.    |
+--------------------------+-------------------------+-------------------------+
|401                       |Unauthorized             |You are not authorized   |
|                          |                         |to complete this         |
|                          |                         |operation. This error    |
|                          |                         |can occur if the request |
|                          |                         |is submitted with an     |
|                          |                         |invalid authentication   |
|                          |                         |token.                   |
+--------------------------+-------------------------+-------------------------+
|403                       |Forbidden                |You are denied access to |
|                          |                         |the requested resource.  |
+--------------------------+-------------------------+-------------------------+
|404                       |Not Found                |The requested item was   |
|                          |                         |not found.               |
+--------------------------+-------------------------+-------------------------+
|405                       |badMethod                |The specified method is  |
|                          |                         |not allowed for the      |
|                          |                         |given resource.          |
+--------------------------+-------------------------+-------------------------+
|413                       |Over Limit               |The number of items      |
|                          |                         |returned is above the    |
|                          |                         |allowed limit.           |
+--------------------------+-------------------------+-------------------------+
|422                       |unprocessableEntity      |The item cannot be       |
|                          |                         |processed.               |
+--------------------------+-------------------------+-------------------------+
|500                       |instanceFault            |The instance has         |
|                          |                         |experienced a fault.     |
+--------------------------+-------------------------+-------------------------+
|501                       |notImplemented           |The server does not      |
|                          |                         |support the              |
|                          |                         |functionality required   |
|                          |                         |to fulfill the request.  |
+--------------------------+-------------------------+-------------------------+
|503                       |Service Unavailable      |The service is not       |
|                          |                         |available.               |
+--------------------------+-------------------------+-------------------------+


Request
""""""""""""""""




This table shows the URI parameters for the request:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|{accountId}               |String                   |The account ID of the    |
|                          |                         |owner of the specified   |
|                          |                         |instance.                |
+--------------------------+-------------------------+-------------------------+
|{haId}                    |String                   |The ID for the specified |
|                          |                         |HA instance.             |
+--------------------------+-------------------------+-------------------------+








**Example Add Replica to an HA instance: JSON request**


The following example shows the Add replica to an HA instance request:

.. code::

   POST /v1.0/1234/ha/e7fdf90b-7140-4edb-b449-e093d55008fb/action HTTP/1.1
   User-Agent: python-troveclient
   Host: ord.databases.api.rackspacecloud.com
   X-Auth-Token: f47d99adabe14bc8bd7bccda88292918
   Accept: application/json
   Content-Type: application/json
    
   {  
      "add_replica":{  
         "replica_details":{  
            "volume":{  
               "size":1
            },
            "flavorRef":"2",
            "name":"new-replica2"
         }
      }
   }
   





Response
""""""""""""""""










**Example Add Replica to an HA instance: JSON response**


The following example shows the Add replica to an HA instance response:

.. code::

   HTTP/1.1 202 Accepted
   Content-Type: application/json
   Via: 1.1 Repose (Repose/2.12)
   Content-Length: 0
   Date: Fri, 31 Jul 2015 16:53:03 GMT
   Connection: close
   Server: Jetty(8.0.y.z-SNAPSHOT)
   




