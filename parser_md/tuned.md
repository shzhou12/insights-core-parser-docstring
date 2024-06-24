Tuned - command ``/usr/sbin/tuned-adm list``
============================================

This parser reads the output of the ``/usr/sbin/tuned-adm list`` command and
reads it into a simple dictionary in the ``data`` property with two of three
keys:

* ``available`` - the list of available profiles
* ``active`` - the active profile name
* ``preset`` - the profile name that's preset to be used when tuned is active

The ``active`` key is available when ``tuned`` is running, because the active
profile is only listed when the daemon is active.  If ``tuned`` is not
running, the tuned-adm command will list the profile that will be used when
the daemon is running, and this is given in the ``preset`` key.

Sample data::

    Available profiles:
    - balanced
    - desktop
    - latency-performance
    - network-latency
    - network-throughput
    - powersave
    - throughput-performance
    - virtual-guest
    - virtual-host
    Current active profile: virtual-guest

Examples:

    >>> type(tuned)
    <class 'insights.parsers.tuned.Tuned'>
    >>> 'active' in tuned
    True
    >>> tuned['active']
    'virtual-guest'
    >>> len(tuned['available'])
    9
    >>> 'balanced' in tuned['available']
    True