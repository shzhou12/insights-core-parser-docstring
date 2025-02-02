BrctlShow - command ``brctl show``
==================================

This module provides processing for the output of the ``brctl show`` command.

Class ``BrctlShow`` parses the output of the ``brctl show`` command.
Sample output of this command looks like::

    ---
    bridge name     bridge id               STP enabled     interfaces
    br0             8000.08002731ddfd       no              eth1
                                                            eth2
                                                            eth3
    br1             8000.0800278cdb62       no              eth4
                                                            eth5
    br2             8000.0800278cdb63       no              eth6
    docker0         8000.0242d4cf2112       no
    ---

Examples:
    >>> brctl_content = '''
    ... bridge name     bridge id               STP enabled     interfaces
    ... br0             8000.08002731ddfd       no              eth1
    ...                                                         eth2
    ...                                                         eth3
    ... br1             8000.0800278cdb62       no              eth4
    ...                                                         eth5
    ... br2             8000.0800278cdb63       no              eth6
    ... docker0         8000.0242d4cf2112       no
    ... '''.strip()
    >>> from insights.parsers.brctl_show import BrctlShow
    >>> from insights.tests import context_wrap
    >>> shared = {BrctlShow: BrctlShow(context_wrap(brctl_content))}
    >>> brctl_info = BrctlShow(context_wrap(brctl_content))
    >>> brctl_info.data
    [
     {'interfaces': ['eth1', 'eth2', 'eth3'], 'bridge id': '8000.08002731ddfd',
      'STP enabled': 'no', 'bridge name': 'br0'},
     {'interfaces': ['eth4', 'eth5'], 'bridge id': '8000.0800278cdb62',
      'STP enabled': 'no', 'bridge name': 'br1'},
     {'interfaces': ['eth6'], 'bridge id': '8000.0800278cdb63',
      'STP enabled': 'no', 'bridge name': 'br2'},
     {'bridge id': '8000.0242d4cf2112', 'STP enabled': 'no',
      'bridge name': 'docker0'}
    ]
    >>> brctl_info.group_by_iface
    {
     'docker0': {'STP enabled': 'no', 'bridge id': '8000.0242d4cf2112'},
     'br2': {'interfaces': ['eth6'], 'STP enabled': 'no',
             'bridge id': '8000.0800278cdb63'},
     'br1': {'interfaces': ['eth4', 'eth5'], 'STP enabled': 'no',
             'bridge id': '8000.0800278cdb62'},
     'br0': {'interfaces': ['eth1', 'eth2', 'eth3'], 'STP enabled': 'no',
             'bridge id': '8000.08002731ddfd'}
    }