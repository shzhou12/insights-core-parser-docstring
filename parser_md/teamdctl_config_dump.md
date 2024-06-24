TeamdctlConfigDump - command ``teamdctl {team interface} config dump``
======================================================================

This module provides processing for the output of the command
``teamdctl {team interface} config dump``.

Attributes:
    data (dict): Dictionary of keys with values in dict.

Sample configuration file::

    {
        "device": "team0",
        "hwaddr": "DE:5D:21:A8:98:4A",
        "link_watch": [
            {
                "delay_up": 5,
                "name": "ethtool"
            },
            {
                "name": "nsna_ping",
                "target_host ": "target.host"
            }
        ],
        "mcast_rejoin": {
            "count": 1
        },
        "notify_peers": {
            "count": 1
        },
        "runner": {
            "hwaddr_policy": "only_active",
            "name": "activebackup"
        }
    }

Examples:
    >>> str(teamdctl_config_dump.device_name)
    'team0'
    >>> str(teamdctl_config_dump.runner_name)
    'activebackup'
    >>> str(teamdctl_config_dump.runner_hwaddr_policy)
    'only_active'