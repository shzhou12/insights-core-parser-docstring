Cgroups - File ``/proc/cgroups``
================================

This parser reads the content of ``/proc/cgroups``.
This file shows the control groups information of system.

Sample ``/proc/cgroups`` file::

    #subsys_name        hierarchy       num_cgroups     enabled
    cpuset      10      48      1
    cpu 2       232     1
    cpuacct     2       232     1
    memory      5       232     1
    devices     6       232     1
    freezer     3       48      1
    net_cls     4       48      1
    blkio       9       232     1
    perf_event  8       48      1
    hugetlb     11      48      1
    pids        7       232     1
    net_prio    4       48      1


Examples:

    >>> i_cgroups.get_num_cgroups("memory")
    232
    >>> i_cgroups.is_subsys_enabled("memory")
    True
    >>> i_cgroups.data[0].get('hierarchy')
    '10'
    >>> i_cgroups.subsystems["memory"]["enabled"]
    '1'