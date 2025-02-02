DnfConf - file ``/etc/dnf/dnf.conf``
====================================

This module provides parsing for the ``/etc/dnf/dnf.conf`` file.
The ``DnfConf`` class parses the information in the file
``/etc/dnf/dnf.conf``. See the ``YumConf`` class for more
information on attributes and methods.

Sample file content::

    [main]
    gpgcheck=1
    installonly_limit=3
    clean_requirements_on_remove=True
    best=False
    skip_if_unavailable=True

Examples:
    >>> 'main' in dconf
    True
    >>> 'rhel-7-server-rpms' in dconf
    False
    >>> dconf.has_option('main', 'gpgcheck')
    True
    >>> dconf.has_option('main', 'foo')
    False