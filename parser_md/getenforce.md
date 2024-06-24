getenforce - command ``/usr/sbin/getenforce``
=============================================

This very simple parser returns the output of the ``getenforce`` command.

Examples:

    >>> enforce = shared[getenforcevalue]
    >>> enforce['status']
    'Enforcing'