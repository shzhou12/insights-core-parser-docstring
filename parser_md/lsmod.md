LsMod - command ``/sbin/lsmod``
===============================

This parser reads the output of ``/sbin/lsmod`` into a dictionary, keyed on
the module name.  Each item is a dictionary with three keys:

* ``size`` - the size of the module's memory footprint in bytes
* ``depnum`` - the number of modules dependent on this module
* ``deplist`` - the list of dependent modules as presented (i.e. as a string)

This dictionary is available in the ``data`` attribute.

The parser also provides pseudo-dictionary access so it can be checked for
the existence of a module or module data retrieved as if it was a dictionary.

Sample input::

    Module                  Size  Used by
    xt_CHECKSUM            12549  1
    ipt_MASQUERADE         12678  3
    nf_nat_masquerade_ipv4    13412  1 ipt_MASQUERADE
    tun                    27141  3
    ip6t_rpfilter          12546  1

Examples:

    >>> modules = shared[LsMod]
    >>> 'ip6t_rpfilter' in modules
    True
    >>> 'bridge' in modules
    False
    >>> modules['tun']['deplist']
    ''
    >>> modules['nf_nat_masquerade_ipv4']['deplist']
    'ipt_MASQUERADE'