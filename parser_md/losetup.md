LoSetup - command ``/usr/sbin/losetup -l``
==========================================

This parser reads the output of ``/usr/sbin/losetup -l`` into a list of entries.
Each entry is a dictionary of headers:

* ``NAME`` - the path name of the loop back device (strings)
* ``SIZELIMIT`` - the data end position of backing file in bytes (integer)
* ``OFFSET`` - the data start position of backing file in bytes (integer)
* ``AUTOCLEAR`` - the autoclear flag (boolean)
* ``RO`` - the read only flag (boolean)
* ``BACK-FILE`` - the path of the backing file (strings)
* ``DIO`` - the direct I/O flag (boolean)
* ``LOG-SEC`` - the logical sector size of the loop device in bytes (integer)

Sample output of ``losetup -l`` command is::

    NAME       SIZELIMIT OFFSET AUTOCLEAR RO BACK-FILE      DIO LOG-SEC
    /dev/loop0         0      0         0  0 /root/disk.img   1     512

Examples:

    >>> type(losetup)
    <class 'insights.parsers.losetup.LoSetup'>
    >>> len(losetup)
    1
    >>> losetup[0]['NAME']
    '/dev/loop0'
    >>> losetup[0]['RO']
    False
    >>> losetup[0]['DIO']
    True
    >>> losetup[0]['NAME']
    '/dev/loop0'
    >>> losetup[0]['SIZELIMIT']
    0
    >>> losetup[0]['OFFSET']
    0
    >>> losetup[0]['AUTOCLEAR']
    False
    >>> losetup[0]['RO']
    False
    >>> losetup[0]['BACK-FILE']
    '/root/disk.img'
    >>> losetup [0]['DIO']
    True
    >>> losetup[0]['LOG-SEC']
    512