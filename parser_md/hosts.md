Hosts - file ``/etc/hosts``
===========================

This parser parses the ``/etc/hosts`` file, strips the comments, ignores the
blank lines, and collects the host names by IP address.  IPv4 and IPv6
addresses are supported.

Sample hosts file::

    127.0.0.1 localhost localhost.localdomain localhost4 localhost4.localdomain4
    ::1 localhost localhost.localdomain localhost6 localhost6.localdomain6
    # The same IP address can appear more than once, with different names
    127.0.0.1 fte.example.com

    10.0.0.1 nonlocal.example.com nonlocal2.fte.example.com
    10.0.0.2 other.host.example.com # Comments at end of line are ignored

Examples:

    >>> len(hosts.all_names)
    10
    >>> 'localhost6'in  hosts.all_names
    True
    >>> hosts.data['127.0.0.1']
    ['localhost', 'localhost.localdomain', 'localhost4', 'localhost4.localdomain4', 'fte.example.com']
    >>> sorted(hosts.get_nonlocal().keys())
    ['10.0.0.1', '10.0.0.2']
    >>> hosts.lines[-1]['ip']
    '10.0.0.2'
    >>> hosts.lines[2]['names']
    ['fte.example.com']