NetworkNamespace = ``/bin/ls /var/run/netns``
=============================================

This specs provides list of network namespace created on the host machine.

Typical output of this command is as below::

    temp_netns  temp_netns_2  temp_netns_3


The ``/bin/ls /var/run/netns`` is prefered over ``/bin/ip netns list`` because it works on
all RHEL versions, no matter ip package is installed or not.

Examples:
    >>> type(netns_obj)
    <class 'insights.parsers.net_namespace.NetworkNamespace'>
    >>> netns_obj.netns_list
    ['temp_netns', 'temp_netns_2', 'temp_netns_3']
    >>> len(netns_obj.netns_list)
    3