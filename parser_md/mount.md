Mount Entries
=============

Parsers provided in this module includes:

Mount - command ``/bin/mount``
------------------------------

ProcMounts - file ``/proc/mounts``
----------------------------------

MountInfo - file ``/proc/self/mountinfo``
-----------------------------------------

The ``Mount`` class implements parsing for the ``mount`` command output which looks like::

    /dev/mapper/rootvg-rootlv on / type ext4 (rw,relatime,barrier=1,data=ordered)
    proc on /proc type proc (rw,nosuid,nodev,noexec,relatime)
    /dev/mapper/HostVG-Config on /etc/shadow type ext4 (rw,noatime,seclabel,stripe=256,data=ordered)
    dev/sr0 on /run/media/root/VMware Tools type iso9660 (ro,nosuid,nodev,relatime,uid=0,gid=0,iocharset=utf8,mode=0400,dmode=0500,uhelper=udisks2) [VMware Tools]

The information is stored as a list of :class:`MountEntry` objects.  Each
:class:`MountEntry` object contains attributes for the following information that
are listed in the same order as in the command output:

 * ``mount_source`` - Name of filesystem or the mounted device
 * ``mount_point`` - Name of mount point for filesystem
 * ``mount_type`` - Name of filesystem type
 * ``mount_options`` -  Mount options as ``MountOpts`` object
 * ``mount_label`` - Optional label of this mount entry, empty string by default
 * ``mount_addtlinfo`` - Additional mount information as ``MountAddtlInfo`` object
 * ``mount_clause`` - Full raw string from command output
 * ``filesystem`` - Name of filesystem or the mounted device (Deprecated)

``ProcMounts`` and ``MountInfo`` classes have the similar style as ``mount``.

MountEntry lines are also available in a ``mounts`` property, keyed on the
mount point.