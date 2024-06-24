SCSIFWver - file ``/sys/class/scsi_host/host[0-9]*/fwrev``
==========================================================

This parser parses the content from fwver file from individual
SCSI hosts. This parser will return data in dictionary format.

Sample Content from ``/sys/class/scsi_host/host0/fwrev``::

    2.02X12 (U3H2.02X12), sli-3


Examples:
    >>> type(scsi_obj)
    <class 'insights.parsers.scsi_fwver.SCSIFWver'>
    >>> scsi_obj.data
    {'host0': ['2.02X12 (U3H2.02X12)', 'sli-3']}
    >>> scsi_obj.scsi_host
    'host0'