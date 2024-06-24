getsebool - command ``/usr/sbin/getsebool -a``
==============================================

This parser returns the output of the ``getsebool``
command.

Sample ``getsebool -a`` output::

    webadm_manage_user_files --> off
    webadm_read_user_files --> off
    wine_mmap_zero_ignore --> off
    xdm_bind_vnc_tcp_port --> off
    ssh_keysign --> off

Examples:

    >>> "webadm_manage_user_files" in getsebool
    True
    >>> "tmpreaper_use_nfs" in getsebool
    False
    >>> getsebool['ssh_keysign']
    'off'