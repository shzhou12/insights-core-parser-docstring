Sat6DBMigrateStatus - command ``foreman-rake db:migrate:status``
================================================================

This parser collects the output of the ``foreman-rake db:migrate:status``
command, which checks the status of all the migrations known to Foreman.
Each migration has a status, a date code, and a name.  These are stored
in a list of migrations, with 'up' migrations being listed in an ``up``
property and migrations with any other status being stored in a ``down``
property.

Sample input::

    database: foreman

     Status   Migration ID    Migration Name
    --------------------------------------------------
       up     20090714132448  Create hosts
       up     20090714132449  Add audits table
       up     20090715143858  Create architectures
       up     20090717025820  Create media
       up     20090718060746  Create domains
       up     20090718064254  Create subnets
       up     20090720134126  Create operatingsystems
       up     20090722140138  Create models

Examples:
    >>> status = shared[Sat6DBMigrateStatus]
    >>> status.database
    'foreman'
    >>> '20090714132448' in status.migrations
    True
    >>> '20090714140138' in status.migrations
    False
    >>> len(status.up)
    8
    >>> status.down
    []