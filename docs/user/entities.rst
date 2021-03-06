.. _entities:

********
Entities
********

Entities describe what you want to monitor in your infrastructure. This can be as basic as a host, with its attributes hostname and IP; or something more complex, like a PostgreSQL sharded cluster with its identifier and set of connection strings.

ZMON gives you two options for autonomation in/integration with your platform: storing entities via zmon-controller_'s entity service, or discovering them via the adapters in zmon-scheduler_. At Zalando we use both, connecting ZMON to tools like our CMDB but also pushing entities via REST API.

ZMON's entity service describes entities with a single JSON document. Any entity must contain an ID that is unique within your ZMON deployment. We often use a pattern like <hostname>(:<port>) to create uniqueness at the host and application levels, but this is up to you.

Examples
--------

In working with the Vagrant Box, you can use the scheduler instance entity like this:

.. code-block:: json

    {
        "id":"localhost:3421",
        "type":"instance",
        "host":"localhost",
        "project":"zmon-scheduler-ng",
        "ports": {"3421":3421},
    }

Here, you can use the "ports" dictionary to also describe additional open ports. As with Spring Boot, a second port is usually added, exposing management features.

Now let's look at an example of the PostgreSQL instance:

.. code-block:: json

    {
        "id":"localhost:5432",
        "type":"database",
        "name":"zmon-cluster",
        "shards": {"zmon":"localhost:5432/local_zmon_db"}
    }

Usage of the property "shards" is given by how ZMON's worker exposes PostgreSQL clusters to the sql() function.

View more examples here_. 

.. _zmon-controller: https://github.com/zalando/zmon-controller
.. _zmon-scheduler: https://github.com/zalando/zmon-scheduler
.. _here: https://github.com/zalando/zmon/tree/master/examples/entities
