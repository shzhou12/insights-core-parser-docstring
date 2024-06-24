NUMACpus - file ``/sys/devices/system/node/node[0-9]*/cpulist``
===============================================================

This parser will parse the content from cpulist file, from individual
NUMA nodes. This parser will return data in (dict) format.

Sample Content from ``/sys/devices/system/node/node0/cpulist``::

    0-6,14-20

Examples:
    >>> type(numa_cpus_obj)
    <class 'insights.parsers.numa_cpus.NUMACpus'>
    >>> numa_cpus_obj.numa_node_name
    'node0'
    >>> numa_cpus_obj.numa_node_details() == {'numa_node_range': ['0-6', '14-20'], 'total_cpus': 14, 'numa_node_name': 'node0'}
    True
    >>> numa_cpus_obj.numa_node_cpus
    ['0-6', '14-20']
    >>> numa_cpus_obj.total_numa_node_cpus
    14