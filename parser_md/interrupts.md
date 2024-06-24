Interrupts - file ``/proc/interrupts``
======================================

Provides parsing for contents of ``/proc/interrupts``.
The contents of a typical ``interrupts`` file looks like::

             CPU0       CPU1       CPU2       CPU3
    0:         37          0          0          0  IR-IO-APIC   2-edge      timer
    1:          3          2          1          0  IR-IO-APIC   1-edge      i8042
    8:          0          1          0          0  IR-IO-APIC   8-edge      rtc0
    9:      11107       2316       4040       1356  IR-IO-APIC   9-fasteoi   acpi
  NMI:        210         92        179         96   Non-maskable interrupts
  LOC:    7561411    2488524    6527767    2448192   Local timer interrupts
  ERR:          0
  MIS:          0

The information is parsed by the ``Interrupts`` class.  The information is stored
as a list of dictionaries in order corresponding to the output.
The counts in the CPU# columns are represented in a ``list``.
The following is a sample of the parsed information stored in an ``Interrupts``
class object::

    [
        { 'irq': '0',
          'num_cpus': 4,
          'counts': [37, 0, 0, 0],


        { 'irq': 'MIS',
          'num_cpus': 4,
          'counts': [0, ]}
    ]

Examples:
    >>> int_info = shared[Interrupts]
    >>> int_info.data[0]
    {'irq': '0', 'num_cpus': 4, 'counts': [37, 0, 0, 0],
     'type_device': 'IR-IO-APIC   2-edge      timer'}
    >>> int_info.num_cpus
    4
    >>> int_info.get('i8042')
    [{'irq': '1', 'num_cpus': 4, 'counts': [3, 2, 1, 0],
      'type_device': 'IR-IO-APIC   1-edge      i8042'}]
    >>> [i['irq'] for i in int_info if i['counts'][0] > 1000]
    ['9', 'LOC']