DumpE2FS - Command ``dumpe2fs -h``
==================================

This parser handles ``dumpe2fs`` output.

The object provides access to this data using a dictionary.  Particular keys
are stored as lists:

* Filesystem features
* Filesystem flags
* Default mount options

Other keys are stored as strings.  The name of the device is stored in the
``dev_name`` property.

Typical contents of the ``/sbin/dumpe2fs -h /dev/device`` command::

    dumpe2fs 1.41.12 (17-May-2010)
    Filesystem volume name:   <none>
    Last mounted on:          /usr
    Filesystem UUID:          1b332c5d-2410-4934-9118-466f8a14841f
    Filesystem magic number:  0xEF53
    Filesystem revision #:    1 (dynamic)
    Filesystem features:      has_journal ext_attr resize_inode dir_index filetype needs_recovery extent flex_bg sparse_super large_file huge_file uninit_bg dir_nlink extra_isize
    Filesystem flags:         signed_directory_hash
    Default mount options:    user_xattr acl

Examples:

    >>> e2fs = shared[DumpE2fs]
    >>> e2fs.dev_name
    '/dev/device'
    >>> e2fs['Filesystem volume name']
    '<none>'
    >>> e2fs['Last mounted on']
    '/usr'
    >>> e2fs['Filesystem UUID']
    '1b332c5d-2410-4934-9118-466f8a14841f'
    >>> e2fs['Filesystem magic number']
    '0xEF53'
    >>> e2fs['Filesystem revision #']
    '1 (dynamic)'
    >>> e2fs['Filesystem features']
    ['has_journal', 'ext_attr', 'resize_inode', 'dir_index', 'filetype',
     'needs_recovery', 'extent', 'flex_bg', 'sparse_super', 'large_file',
     'huge_file', 'uninit_bg', 'dir_nlink', 'extra_isize'],
    >>> e2fs['Filesystem flags']
    ['signed_directory_hash']
    >>> e2fs['Default mount options']
    ['user_xattr', 'acl']