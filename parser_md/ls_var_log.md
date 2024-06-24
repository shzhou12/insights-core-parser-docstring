LsVarLog - command ``ls -laR /var/log``
=======================================

This parser reads the ``/var/log`` directory listings and uses the FileListing
parser class to provide a common access to them.

Examples:

    >>> varlog = shared[LsVarLog]
    >>> '/var/log' in varlog
    True
    >>> varlog.dir_contains('/var/log', 'messages')
    True
    >>> messages = varlog.dir_entry('/var/log', 'messages')
    >>> messages['type']
    '-'
    >>> messages['perms']
    'rw-------'