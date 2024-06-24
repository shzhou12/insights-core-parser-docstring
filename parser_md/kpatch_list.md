KpatchList - command ``/usr/sbin/kpatch list``
==============================================

The ``/usr/sbin/kpatch list`` command provides information about
the installed patch modules.

Sample content from command ``/usr/sbin/kpatch list`` is::
    Loaded patch modules:
    kpatch_3_10_0_1062_1_1_1_4 [enabled]

    Installed patch modules:
    kpatch_3_10_0_1062_1_1_1_4 (3.10.0-1062.1.1.el7.x86_64)

Examples:
    >>> 'kpatch_3_10_0_1062_1_1_1_4' in kpatchs.loaded
    True
    >>> kpatchs.loaded.get('kpatch_3_10_0_1062_1_1_1_4')
    'enabled'
    >>> 'kpatch_3_10_0_1062_1_1_1_4' in kpatchs.installed
    True
    >>> kpatchs.installed.get('kpatch_3_10_0_1062_1_1_1_4')
    '3.10.0-1062.1.1.el7.x86_64'