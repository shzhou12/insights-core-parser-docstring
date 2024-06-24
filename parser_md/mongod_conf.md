MongodbConf - files - Configuration files for MongoDB
=====================================================

This module contains the following files:
    ``/etc/mongod.conf``,
    ``/etc/mongodb.conf`` ,
    ``/etc/opt/rh/rh-mongodb26/mongod.conf``
    ``/etc/opt/rh/rh-mongodb34/mongod.conf``

They are provided by package mongodb-server, rh-mongodb26-mongodb-server or
rh-mongodb34-mongodb-server.
These MongoDB configuration files may use the **YAML** format
or the standard **key-value pair** format.


Sample input(YAML format)::

    systemLog:
      destination: file
      logAppend: true
      path: /var/log/mongodb/mongod.log

    # Where and how to store data.
    storage:
      dbPath: /var/lib/mongo
      journal:
        enabled: true


Sample input(key-value pair format)::

    # mongodb.conf - generated from Puppet
    #where to log
    logpath=/var/log/mongodb/mongodb.log
    logappend=true
    # Set this option to configure the mongod or mongos process to bind to and
    # listen for connections from applications on this address.
    # You may concatenate a list of comma separated values to bind mongod to multiple IP addresses.
    bind_ip = 127.0.0.1
    # fork and run in background
    fork=true
    dbpath=/var/lib/mongodb
    # location of pidfile
    pidfilepath=/var/run/mongodb/mongodb.pid
    # Enables journaling
    journal = true
    # Turn on/off security.  Off is currently the default
    noauth=true


Examples:

    >>> mongod_conf1 = shared[MongodConf]
    >>> mongod_conf2 = shared[MongodConf]
    >>> MongodbConf1.is_yaml
    True
    >>> MongodbConf2.is_yaml
    False
    >>> mongod_conf1.fork
    True
    >>> mongod_conf2.fork
    'true'
    >>> mongod_conf1.dbpath
    '/var/lib/mongo'
    >>> mongod_conf2.dbpath
    '/var/lib/mongo'
    >>> mongod_conf1.get("systemlog", {}).get("logAppend")
    True
    >>> MongodbConf2.get("logappend")
    'true'