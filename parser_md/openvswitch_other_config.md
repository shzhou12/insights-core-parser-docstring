OpenvSwitchOtherConfig - command ``ovs-vsctl -t 5 get Open_vSwitch . other_config``
===================================================================================

Class OpenvSwitchOtherConfig process the output of the following OpenvSwitch command:

ovs-vsctl -t 5 get Open_vSwitch . other_config


Sample input::

    {dpdk-init="true", dpdk-lcore-mask="30000003000", dpdk-socket-mem="4096,4096", pmd-cpu-mask="30000003000"}

Examples:

    >>> type(ovs_other_conf)
    <class 'insights.parsers.openvswitch_other_config.OpenvSwitchOtherConfig'>
    >>> ovs_other_conf.get("dpdk-init")
    true
    >>> ovs_other_conf["dpdk-lcore-mask"]
    30000003000
    >>> dpdk-socket-mem in ovs_other_conf
    True