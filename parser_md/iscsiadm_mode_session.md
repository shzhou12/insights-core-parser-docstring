IscsiAdmModeSession - command ``iscsiadm - m session``
======================================================

This module provides the class ``IscsiAdmModeSession`` which processes
``iscsiadm -m session`` command output.  Typical output looks like::

    tcp: [1] 10.72.32.45:3260,1 iqn.2017-06.com.example:server1 (non-flash)
    tcp: [2] 10.72.32.45:3260,1 iqn.2017-06.com.example:server2 (non-flash)

The class has one attribute ``data`` which is a ``list`` representing each line
of the input data as a ``dict`` with keys corresponding to the keys in the output.

Examples:

    >>> iscsiadm_mode_session_content = '''
    ... tcp: [1] 10.72.32.45:3260,1 iqn.2017-06.com.example:server1 (non-flash)
    ... tcp: [2] 10.72.32.45:3260,1 iqn.2017-06.com.example:server2 (non-flash)
    ...'''.strip()

    >>> from insights.parsers.iscsiadm_mode_session import IscsiAdmModeSession
    >>> from insights.tests import context_wrap
    >>> shared = {IscsiAdmModeSession: IscsiAdmModeSession(context_wrap(iscsiadm_mode_session_content))}
    >>> result = shared[IscsiAdmModeSession]
    >>> result[0]
    {'IFACE_TRANSPORT': 'tcp', 'SID': '1', 'TARGET_IP': '10.72.32.45:3260,1',
     'TARGET_IQN': 'iqn.2017-06.com.example:server1'}
    >>> result[1]['TARGET_IQN']
    'iqn.2017-06.com.example:server2'