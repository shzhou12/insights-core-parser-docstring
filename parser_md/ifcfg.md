IfCFG - files ``/etc/sysconfig/network-scripts/ifcfg-*``
========================================================

IfCFG is a parser for the network interface definition files in
``/etc/sysconfig/network-scripts``.  These are pulled into the network
scripts using ``source``, so they are mainly ``bash`` environment
declarations of the form **KEY=value**.  These are stored in the ``data``
property as a dictionary.  Quotes surrounding the value

Three options are handled differently:

* ``BONDING_OPTS`` is usually a quoted list of key=value arguments separated
  by spaces.
* ``TEAM_CONFIG`` and ``TEAM_PORT_CONFIG`` are treated as JSON stored as a
  single string.  Double quotes within the string are escaped using double
  back slashes, and these are removed so that the quoting is preserved.

Because this parser reads multiple files, the interfaces are stored as a
list within the parser and need to be iterated through in order to find
specific interfaces.

Sample configuration from a teamed interface in file ``/etc/sysconfig/network-scripts/ifcfg-team1``::

    DEVICE=team1
    DEVICETYPE=Team
    ONBOOT=yes
    NETMASK=255.255.252.0
    IPADDR=192.168.0.1
    TEAM_CONFIG='{"runner": {"name": "lacp", "active": "true", "tx_hash": ["eth", "ipv4"]}, "tx_balancer": {"name": "basic"}, "link_watch": {"name": "ethtool"}}'

Examples:

    >>> for nic in shared[IfCFG]: # Parser contains list of all interfaces
    ...     print 'NIC:', nic.iname
    ...     print 'IP address:', nic['IPADDR']
    ...     if 'TEAM_CONFIG' in nic:
    ...         print 'Team runner name:', nic['TEAM_CONFIG']['runner']['name']
    ...
    NIC: team1
    IP addresss: 192.168.0.1
    Team runner name: lacp