Uname - command ``uname -a``
============================

The ``Uname`` class reads the output of the ``uname -a`` command and
interprets it.  It also does a number of handy extra things, like deriving
the RHEL release from the kernel version.

Uname objects can also be compared by their kernel versions.

An example from the following ``uname -a`` output::

    Linux server1.example.com 2.6.32-504.el6.x86_64 #1 SMP Tue Sep 16 01:56:35 EDT 2014 x86_64 x86_64 x86_64 GNU/Linux

Example:

    >>> type(uname)
    <class 'insights.parsers.uname.Uname'>
    >>> uname.version
    '2.6.32'
    >>> uname.release
    '504.el6'
    >>> uname.arch
    'x86_64'
    >>> uname.nodename
    'server1.example.com'

Uname objects can be created from, and compared to, other Uname objects or
kernel strings::

    >>> early_rhel6 = Uname.from_kernel('2.6.32-71')
    >>> late_rhel6 = Uname.from_release('6.7')
    >>> late_rhel6 > early_rhel6
    True
    >>> early_rhel6 > '2.6.32-279.el6.x86_64'
    False