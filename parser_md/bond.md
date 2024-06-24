Bond - file ``/proc/net/bonding``
=================================

Provides plugins access to the network bonding information gathered from
all the files starteing with "bond." located in the
``/proc/net/bonding`` directory.

Typical content of ``bond.*`` file is::

    Ethernet Channel Bonding Driver: v3.2.4 (January 28, 2008)

    Bonding Mode: IEEE 802.3ad Dynamic link aggregation
    Transmit Hash Policy: layer2 (0)
    MII Status: up
    MII Polling Interval (ms): 500
    Up Delay (ms): 0
    Down Delay (ms): 0

    802.3ad info
    LACP rate: slow
    Active Aggregator Info:
            Aggregator ID: 3
            Number of ports: 1
            Actor Key: 17
            Partner Key: 1
            Partner Mac Address: 00:00:00:00:00:00

    Slave Interface: eth1
    MII Status: up
    Link Failure Count: 0
    Permanent HW addr: 00:16:35:5e:42:fc
    Aggregator ID: 3

    Slave Interface: eth2
    MII Status: up
    Link Failure Count: 0
    Permanent HW addr: 00:16:35:5e:02:7e
    Aggregator ID: 2

Data is modeled as an array of ``Bond`` objects (``bond`` being a
pattern file specification gathering data from files located in
``/proc/net/bonding``.

Examples:
    >>> type(bond_info)
    <class 'insights.parsers.bond.Bond'>
    >>> bond_info.bond_mode
    '4'
    >>> bond_info.partner_mac_address
    '00:00:00:00:00:00'
    >>> bond_info.slave_interface
    ['eth1', 'eth2']
    >>> bond_info.aggregator_id
    ['3', '3', '2']
    >>> bond_info.xmit_hash_policy
    'layer2'
    >>> bond_info.active_slave
    >>> bond_info.slave_duplex
    ['full', 'full']
    >>> bond_info.slave_speed
    ['1000 Mbps', '1000 Mbps']