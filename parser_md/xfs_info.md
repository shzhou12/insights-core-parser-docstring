XFSInfo - command ``/usr/sbin/xfs_info {mount}``
================================================

The ``XFSInfo`` parser reads the output of the ``xfs_info`` command and turns
it into a dictionary of keys and values in several sections, as given in the
output of the command::

     meta-data=/dev/sda      isize=256    agcount=32, agsize=16777184 blks
              =              sectsz=512   attr=2
     data     =              bsize=4096   blocks=536869888, imaxpct=5
              =              sunit=32     swidth=128 blks
     naming   =version 2     bsize=4096
     log      =internal      bsize=4096   blocks=32768, version=2
              =              sectsz=512   sunit=32 blks, lazy-count=1
     realtime =none          extsz=524288 blocks=0, rtextents=0

The main sections are ``meta-data``, ``data``, ``naming``, ``log`` and
``realtime``, stored under those keys in the object's ``xfs_info`` property.
Each section can optionally have a '**specifier**', which is the first thing
after the section name (e.g. ``version`` or ``/dev/sda``).  If no specifier
is found on the line, none is recorded for the section.  The specifier can
also have a value (e.g. ``2`` for the version), which is recorded in the
``specifier_value`` key in the section.

Each 'key=value' pair until the next given section start (or end of file), is
recorded as an entry in the section dictionary, with all values that are
numeric being converted to integers (i.e. usually anything without a '`blks`'
suffix).

Because the spec for this parser can collect multiple files, the shared
parser information contains a list of XFSInfo objects, one per file system.

In addition, the ``data_size`` and ``log_size`` values are calculated as
properties from the block size and blocks in the data and log, respectively.

Attributes:
    xfs_info(dict): A dictionary of dictionaries containing the data from
        the report, keyed on the five section names in the output:
        '``meta-data``', '``data``', '``naming``', '``log``', and
        '``realtime``'.  '``meta-data``', '``data``' and '``log``' are
        always present.  Within each dictionary a special key
        '``specifier``' stores any data immediately after the section
        name - e.g. '/dev/sda' or 'version' in the case of the output
        below.  Any data immediately following that is stored in the
        ``specifier_value`` key.  Otherwise, data is read in key=value
        pairs - e.g. from the output below, the ``isize`` key will have
        the value ``32`` (an integer).  Data values given in blocks are
        left as is, so the value of the ``agsize`` key is '16777184 blks'
        as a string.
    mount(str): If the mount point can be derived from the file name of
        the original output, then this attribute contains the
        reconstructed mount point name.
    device(str): The device name immediately after the '``meta-data``'
        section heading.
    data_size(int): The size of the data segment in bytes, from
        multiplying the ``blocks`` and ``bsize`` values of the ``data``
        section together.
    log_size(int): The size of the log segment in bytes, from multiplying
        the ``blocks`` and ``bsize`` values of the ``log`` section
        together.

Sample output (from file '``sos_commands/xfs/xfs_info_.data``')::

     meta-data=/dev/sda      isize=256    agcount=32, agsize=16777184 blks
              =              sectsz=512   attr=2
     data     =              bsize=4096   blocks=536869888, imaxpct=5
              =              sunit=32     swidth=128 blks
     naming   =version 2     bsize=4096
     log      =internal      bsize=4096   blocks=32768, version=2
              =              sectsz=512   sunit=32 blks, lazy-count=1
     realtime =none          extsz=524288 blocks=0, rtextents=0

Examples:

    >>> xfs = shared[XFSInfo][0]  # first XFS filesystem as an example
    >>> xfs.xfs_info['meta-data']['specifier']
    '/dev/sda'
    >>> 'specifier_value' in xfs.xfs_info['meta-data']
    False
    >>> xfs.xfs_info['meta-data']['agcount']
    32
    >>> xfs.xfs_info['meta-data']['agsize']
    '16777184 blks'
    >>> xfs.data_size
    2199019061248
    >>> 'crc' in xfs.xfs_info['data']
    False