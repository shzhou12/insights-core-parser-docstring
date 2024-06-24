RedhatRelease - File ``/etc/redhat-release``
============================================

This module provides plugins access to file ``/etc/redhat-release``

Typical content of file ``/etc/redhat-release`` is::

    Red Hat Enterprise Linux Server release 7.2 (Maipo)

This module parses the file contents and stores data in the class
attributes described below.

Examples:
    >>> type(rh_release)
    <class 'insights.parsers.redhat_release.RedhatRelease'>
    >>> rh_release.raw
    'Red Hat Enterprise Linux Server release 7.2 (Maipo)'
    >>> rh_release.major
    7
    >>> rh_release.minor
    2
    >>> rh_release.version
    '7.2'
    >>> rh_release.is_rhel
    True
    >>> rh_release.product
    'Red Hat Enterprise Linux Server'