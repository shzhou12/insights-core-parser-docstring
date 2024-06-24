Pmrep - command ``pmrep -t 1s -T 1s <metrics> -o csv``
======================================================

Parse the content of the ``pmrep -t 1s -T 1s network.interface.out.packets network.interface.collisions swap.pagesout mssql.memory_manager.stolen_server_memory mssql.memory_manager.total_server_memory -o csv`` command.

Sample ``pmrep -t 1s -T 1s network.interface.out.packets network.interface.collisions swap.pagesout -o csv`` command output::

    Time,"network.interface.out.packets-lo","network.interface.out.packets-eth0","network.interface.collisions-lo","network.interface.collisions-eth0","swap.pagesout"
    2021-04-26 05:42:24,,,,,
    2021-04-26 05:42:25,1.000,2.000,3.000,4.000,5.000

Examples:
    >>> type(pmrep_doc_obj)
    <class 'insights.parsers.pmrep.PMREPMetrics'>
    >>> pmrep_doc_obj = sorted(pmrep_doc_obj, key=lambda x: x['name'])
    >>> pmrep_doc_obj[3]
    {'name': 'network.interface.collisions-eth0', 'value': '4.000'}
    >>> pmrep_doc_obj[6]
    {'name': 'network.interface.out.packets-lo', 'value': '1.000'}
    >>> pmrep_doc_obj[7]
    {'name': 'swap.pagesout', 'value': '5.000'}