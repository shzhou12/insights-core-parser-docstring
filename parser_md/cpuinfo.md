CpuInfo - file ``/proc/cpuinfo``
================================

This parser reads the content of the ``/proc/cpuinfo`` file and parses it
into a dictionary of lists, keyed on the left hand column of the cpuinfo
output.

The object also provides properties for the standard information about the
CPU and motherboard architecture.

Sample input::

    processor       : 0
    vendor_id       : GenuineIntel
    cpu family      : 6
    model           : 45
    model name      : Intel(R) Xeon(R) CPU E5-2690 0 @ 2.90GHz
    stepping        : 2
    microcode       : 1808
    cpu MHz         : 2900.000
    cache size      : 20480 KB
    physical id     : 0
    siblings        : 1
    core id         : 0
    cpu cores       : 1
    apicid          : 0
    flags           : fpu vme de pse tsc msr pae mce
    address sizes   : 40 bits physical, 48 bits virtual
    bugs            : cpu_meltdown spectre_v1 spectre_v2 spec_store_bypass l1tf mds swapgs taa itlb_multihit

    processor       : 1
    vendor_id       : GenuineIntel
    cpu family      : 6
    model           : 45
    model name      : Intel(R) Xeon(R) CPU E5-2690 0 @ 2.90GHz
    stepping        : 2
    microcode       : 1808
    cpu MHz         : 2900.000
    cache size      : 20480 KB
    physical id     : 2
    siblings        : 1
    core id         : 0
    cpu cores       : 1
    apicid          : 2
    flags           : fpu vme de pse tsc msr pae mce
    address sizes   : 40 bits physical, 48 bits virtual
    bugs            : cpu_meltdown spectre_v1 spectre_v2 spec_store_bypass l1tf mds swapgs taa itlb_multihit

Examples:

    >>> cpu_info.cpu_count
    2
    >>> sorted(cpu_info.apicid)
    ['0', '2']
    >>> cpu_info.socket_count
    2
    >>> cpu_info.vendor
    'GenuineIntel'
    >>> "fpu" in cpu_info.flags
    True
    >>> cpu_info.model_name
    'Intel(R) Xeon(R) CPU E5-2690 0 @ 2.90GHz'
    >>> cpu_info.get_processor_by_index(0)['cpus']
    '0'
    >>> cpu_info.get_processor_by_index(0)['vendors']
    'GenuineIntel'
    >>> cpu_info.microcode
    '1808'