SCSIEhDead - file ``/sys/class/scsi_host/host[0-9]*/eh_deadline``
=================================================================

This parser parses the content from eh_deadline file from
individual SCSI hosts. This parser will return data in
dictionary format.

Sample content from ``/sys/class/scsi_host/host0/eh_deadline``::

    off/10/-1/0

Examples:
    >>> type(scsi_obj0)
    <class 'insights.parsers.scsi_eh_deadline.SCSIEhDead'>
    >>> scsi_obj0.data
    {'host0': 'off'}
    >>> scsi_obj0.scsi_host
    'host0'
    >>> type(scsi_obj1)
    <class 'insights.parsers.scsi_eh_deadline.SCSIEhDead'>
    >>> scsi_obj1.data
    {'host1': '10'}
    >>> scsi_obj1.scsi_host
    'host1'
    >>> type(scsi_obj2)
    <class 'insights.parsers.scsi_eh_deadline.SCSIEhDead'>
    >>> scsi_obj2.data
    {'host2': '-1'}
    >>> scsi_obj2.scsi_host
    'host2'