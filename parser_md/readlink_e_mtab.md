ReadLinkEMtab - command ``readlink -e /etc/mtab``
=================================================

The ``readlink -e /etc/mtab`` command provides information about
the path of ``mtab`` file.

Sample content from command ``readlink -e /etc/mtab`` is::
    /proc/4578/mounts

Examples:
    >>> mtab.path
    '/proc/4578/mounts'