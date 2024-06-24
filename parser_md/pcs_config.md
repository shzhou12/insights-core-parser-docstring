PCSConfig - command ``pcs config``
==================================

This module provides class ``PCSConfig`` for parsing output of ``pcs config`` command.

Typical ``/usr/sbin/pcs config`` output looks something like::

    Cluster Name: cluster-1
    Corosync Nodes:
     node-1 node-2
    Pacemaker Nodes:
     node-1 node-2

    Resources:
     Clone: clone-1
     Meta Attrs: interleave=true ordered=true
     Resource: res-1 (class=ocf provider=pacemaker type=controld)
      Operations: start interval=0s timeout=90 (dlm-start-interval-0s)
                  stop interval=0s timeout=100 (dlm-stop-interval-0s)
                  monitor interval=30s on-fail=fence (dlm-monitor-interval-30s)
     Group: grp-1
     Resource: res-1 (class=ocf provider=heartbeat type=IPaddr2)
      Attributes: ip=10.0.0.1 cidr_netmask=32
      Operations: monitor interval=120s (ip_monitor-interval-120s)
                  start interval=0s timeout=20s (ip_-start-interval-0s)
                  stop interval=0s timeout=20s (ip_-stop-interval-0s)

    Stonith Devices:
    Fencing Levels:

    Location Constraints:
    Resource: fence-1
        Disabled on: res-mgt (score:-INFINITY) (id:location-fence-1--INFINITY)
    Resource: res-1
        Enabled on: res-mcast (score:INFINITY) (role: Started) (id:cli-prefer-res)
    Ordering Constraints:
    Colocation Constraints:

    Resources Defaults:
     resource-stickiness: 100
     migration-threshold: 3
    Operations Defaults:
     No defaults set

    Cluster Properties:
     cluster-infrastructure: corosync
     cluster-name: cluster-1
     dc-version: 1.1.13-10.el7_2.4-44eb2dd
     have-watchdog: false
     no-quorum-policy: ignore
     stonith-enable: true
     stonith-enabled: false

The class provides attribute ``data`` as dictionary with lines parsed line by line based on keys, which are
the key words of the output.
Information in keys ``Corosync Nodes`` and ``Pacemaker Nodes`` is parsed in one line.
The get method ``get(str)`` provides lines from ``data`` based on given key.

Examples:
    >>> pcs_config.get("Cluster Name")
    'cluster-1'
    >>> pcs_config.get("Corosync Nodes")
    ['node-1', 'node-2']
    >>> pcs_config.get("Cluster Properties")
    ['cluster-infrastructure: corosync', 'cluster-name: cluster-1', 'dc-version: 1.1.13-10.el7_2.4-44eb2dd', 'have-watchdog: false', 'no-quorum-policy: ignore', 'stonith-enable: true', 'stonith-enabled: false']
    >>> pcs_config.get("Colocation Constraints")
    ['clone-1 with clone-x (score:INFINITY) (id:clone-INFINITY)', 'clone-2 with clone-x (score:INFINITY) (id:clone-INFINITY)']
    >>> 'have-watchdog' in pcs_config.cluster_properties
    True
    >>> pcs_config.cluster_properties.get('have-watchdog')
    'false'