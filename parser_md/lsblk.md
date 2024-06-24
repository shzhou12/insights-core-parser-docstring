Block device listing
====================

Module for processing output of the ``lsblk`` command.  Different information
is provided by the ``lsblk`` command depending upon the options.  Parsers
included here are:

LSBlock - Command ``lsblk``
---------------------------

The ``LSBlock`` class parses output of the ``lsblk`` command with no options.

LSBlockPairs - Command ``lsblk -P -o [columns...]``
---------------------------------------------------

The ``LSBlockPairs`` class parses output of the ``lsblk -P -o [columns...]``
command.

These classes based on ``BlockDevices`` which implements all of the
functionality except the parsing of command specific information.
Information is stored in the attribute ``self.rows`` which is a ``list`` of
``BlockDevice`` objects.

Each ``BlockDevice`` object provides the functionality for one row of data from the
command output.  Data in a ``BlockDevice`` object is accessible by multiple methods.
For example the NAME field can be accessed in the following four ways::

    lsblk_info.rows[0].data['NAME']
    lsblk_info.rows[0].NAME
    lsblk_info.rows[0].name
    lsblk_info.rows[0].get('NAME')

Sample output of the ``lsblk`` command looks like::

    NAME          MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
    vda           252:0    0    9G  0 disk
    |-vda1        252:1    0  500M  0 part /boot
    `-vda2        252:2    0  8.5G  0 part
      |-rhel-root 253:0    0  7.6G  0 lvm  /
      |-rhel-swap 253:1    0  924M  0 lvm  [SWAP]
    sda             8:0    0  500G  0 disk
    `-sda1          8:1    0  500G  0 part /data

Note the hierarchy demonstrated in the name column. For instance ``vda1`` and
``vda2`` are children of ``vda``.  Likewise, ``rhel-root`` and ``rhel-swap``
are children of ``vda2``.  This relationship is demonstrated in the
``PARENT_NAMES`` key, which is only present if the row is a *child* row.  For
example ``PARENT_NAMES`` value for ``rhel-root`` will be ``['vda', 'vda2']``
meaning that ``vda2`` is the immediate parent and ``vda`` is parent of
``vda2``.

Also note that column names that are not valid Python property names been
changed.  For example ``MAJ:MIN`` has been changed to ``MAJ_MIN``.

Examples:
    >>> lsblk_info = shared[LSBlock]
    >>> lsblk_info
    <insights.parsers.lsblk.LSBlock object at 0x7f1f6a422d50>
    >>> lsblk_info.rows
    [disk:vda,
     part:vda1(/boot),
     part:vda2,
     lvm:rhel-root(/),
     lvm:rhel-swap([SWAP]),
     disk:sda,
     part:sda1(/data)]
    >>> lsblk_info.rows[0]
    disk:vda
    >>> lsblk_info.rows[0].data
    {'READ_ONLY': False, 'NAME': 'vda', 'REMOVABLE': False, 'MAJ_MIN': '252:0',
     'TYPE': 'disk', 'SIZE': '9G'}
    >>> lsblk_info.rows[0].data['NAME']
    'vda'
    >>> lsblk_info.rows[0].NAME
    'vda'
    >>> lsblk_info.rows[0].name
    'vda'
    >>> lsblk_info.rows[0].data['MAJ_MIN']
    '252:0'
    >>> lsblk_info.rows[0].MAJ_MIN
    '252:0'
    >>> lsblk_info.rows[0].maj_min
    '252:0'
    >>> lsblk_info.rows[0].removable
    False
    >>> lsblk_info.rows[0].read_only
    False
    >>> lsblk_info.rows[2].data
    {'READ_ONLY': False, 'PARENT_NAMES': ['vda'], 'NAME': 'vda2',
     'REMOVABLE': False, 'MAJ_MIN': '252:2', 'TYPE': 'part', 'SIZE': '8.5G'}
    >>> lsblk_info.rows[2].parent_names
    ['vda']
    >>> lsblk_info.rows[3].parent_names
    ['vda', 'vda2']
    >>> lsblk_info.device_data['vda'] # Access devices by name
    'disk:vda'
    >>> lsblk_info.search(NAME='vda2')
    [{'READ_ONLY': False, 'PARENT_NAMES': ['vda'], 'NAME': 'vda2',
     'REMOVABLE': False, 'MAJ_MIN': '252:2', 'TYPE': 'part', 'SIZE': '8.5G'}]