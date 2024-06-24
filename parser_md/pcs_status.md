PCSStatus - command ``pcs status``
==================================

This module provides the classs ``PCSStatus`` which processes
``/usr/sbin/pcs status`` command output. Typical output of the ``pcs status``
command looks like::

    Cluster name: mycluster
    Last updated: Thu Dec  1 02:33:50 2016              Last change: Wed Aug  3 03:47:11 2016 by root via cibadmin on nodea.example.com
    Stack: corosync
    Current DC: nodea.example.com (version 1.1.13-10.el7-44eb2dd) - partition WITHOUT quorum
    3 nodes and 3 resources configured

    Online: [ nodea.example.com ]
    OFFLINE: [ nodeb.example.com nodec.example.com ]

    Full list of resources:
        myfence (stonith:fence_xvm):    Stopped
        Resource Group: myweb
            webVIP      (ocf::heartbeat:IPaddr2):       Stopped
            webserver   (ocf::heartbeat:apache):        Stopped
    PCSD Status:
        nodea.example.com: Online
        nodeb.example.com: Offline
        nodec.example.com: Offline
    Daemon Status:
        corosync: active/enabled
        pacemaker: active/enabled
        pcsd: active/enabled

The class ``PCSStatus`` has one attribute ``nodes`` whick is a list containing all
node names that from ``PCSD Status`` section.


Examples:

    >>> pcsstatus_content = '''
    ... Cluster name: openstack
    ... Last updated: Fri Oct 14 15:45:32 2016
    ... Last change: Thu Oct 13 20:02:27 2016
    ... Stack: corosync
    ... Current DC: myhost15 (1) - partition with quorum
    ... Version: 1.1.12-a14efad
    ... 3 Nodes configured
    ... 143 Resources configured
    ... online: [ myhost15 myhost16 myhost17 ]
    ... Full list of resources:
    ... stonith-ipmilan-10.24.221.172   (stonith:fence_ipmilan):        Started myhost15
    ... stonith-ipmilan-10.24.221.171   (stonith:fence_ipmilan):        Started myhost16
    ... stonith-ipmilan-10.24.221.173   (stonith:fence_ipmilan):        Started myhost15
    ... PCSD Status:
    ...     myhost15: Online
    ...     myhost17: Online
    ...     myhost16: Online
    ... Daemon Status:
    ...    corosync: active/enabled
    ...    pacemaker: active/enabled
    ...    pcsd: active/enabled
    ... '''.strip()
    >>> from insights.tests import context_wrap
    >>> shared = {PCSStatus: PCSStatus(context_wrap(pcsstatus_content))}
    >>> pcsstatus_info = shared[PCSStatus]
    >>> pcsstatus_info.get("Cluster name")
    'openstack'
    >>> pcsstatus_info.get("Stack")
    'corosync'
    >>> pcsstatus_info.get("Nodes configured")
    '3'
    >>> pcsstatus_info.get("Resources configured")
    '143'
    >>> pcsstatus_info.nodes
    ['myhost15', 'myhost17', 'myhost16']
    >>> len(pcsstatus_info.get("Full list of resources"))
    3