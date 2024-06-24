VDSMId - file ``/etc/vdsm/vdsm.id``
===================================

Module for parsing the content of file ``vdsm.id``, which is a simple file.

Typical content of "vdsm.id" is::

    # VDSM UUID info
    #
    F7D9D983-6233-45C2-A387-9B0C33CB1306

Examples:
    >>> vd = shared[VDSMId]
    >>> vd.uuid
    "F7D9D983-6233-45C2-A387-9B0C33CB1306"