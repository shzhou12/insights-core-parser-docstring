FirewallDConf - file ``/etc/firewalld/firewalld.conf``
======================================================

The FirewallDConf class parses the file ``/etc/firewalld/firewalld.conf``.
And returns a dict contains the firewall configurations.

Examples:

    >>> type(firewalld)
    <class 'insights.parsers.firewall_config.FirewallDConf'>
    >>> 'DefaultZone' in firewalld
    True
    >>> firewalld['DefaultZone']
    'public'