RhospRelease - file ``/etc/rhosp-release``
==========================================

This module provides plugins access to file ``/etc/rhosp-release``

Typical content of file ``/etc/rhosp-release`` is::

    Red Hat OpenStack Platform release 14.0.0 RC (Rocky)

This module parses the file content and stores data in the dict ``self.release``
with keys ``product``, ``version``, and ``code_name``.

Examples:
    >>> release.product
    'Red Hat OpenStack Platform'
    >>> release.version
    '14.0.0'
    >>> release.code_name
    'Rocky'