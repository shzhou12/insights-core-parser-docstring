MulticastQuerier - command ``find /sys/devices/virtual/net/ -name multicast_querier -print -exec cat {} \;``
============================================================================================================

This module provides processing for the output of the
``find -name multicast_querier ...`` command.

Sample output of this command looks like::

    /sys/devices/virtual/net/br0/bridge/multicast_querier
    0
    /sys/devices/virtual/net/br1/bridge/multicast_querier
    1
    /sys/devices/virtual/net/br2/bridge/multicast_querier
    0

The ``bri_val`` method is to return a dictionary contains bridge interface and
its multicast_querier value as the parsing result::

{'br0': 0, 'br1': 1, 'br2': 0}

Examples:
    >>> multicast_querier_content = '''
    ... /sys/devices/virtual/net/br0/bridge/multicast_querier
    ... 0
    ... /sys/devices/virtual/net/br1/bridge/multicast_querier
    ... 1
    ... /sys/devices/virtual/net/br2/bridge/multicast_querier
    ... 0
    ... '''.strip()
    >>> from insights.tests import context_wrap
    >>> from insights.parsers.multicast_querier import MulticastQuerier
    >>> shared = {MulticastQuerier: MulticastQuerier(context_wrap(multicast_querier_content))}
    >>> mq_results = MulticastQuerier(context_wrap(multicast_querier_content))
    >>> mq_results.bri_val
    {'br0': 0, 'br1': 1, 'br2': 0}