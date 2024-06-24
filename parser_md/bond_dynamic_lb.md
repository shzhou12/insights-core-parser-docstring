BondDynamicLB - file ``/sys/class/net/bond[0-9]*/bonding/tlb_dynamic_lb``
=========================================================================

This file represent weather the transmit load balancing is enabled or not

tlb_dynamic_lb=1 mode:
    The outgoing traffic is distributed according to the current load.

tlb_dynamic_lb=0 mode:
    The load balancing based on current load is disabled and the load
    is distributed only using the hash distribution.

Typical content of the file is::

        1

Data is modeled as an array of ``BondDynamicLB`` objects

Examples:
    >>> type(tlb_bond)
    <class 'insights.parsers.bond_dynamic_lb.BondDynamicLB'>
    >>> tlb_bond.dynamic_lb_status
    1
    >>> tlb_bond.bond_name
    'bond0'