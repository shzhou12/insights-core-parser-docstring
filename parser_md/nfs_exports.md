NFS exports configuration
=========================

NFSExports and NFSExportsD provide a parsed output of the content of an exports
file as defined in ``man exports(5)``.  The content is parsed into a
dictionary, where the key is the export path and the value is another
dictionary, where the key is the hostname and the value is the option list,
parsed into an actual list.

The default (``"-"``) hostname is not specially handled, nor are wildcards.

If export paths are defined multiple times in a file, only the first one is
parsed.  All subsequent redefinitions are not parsed and the raw line is added
to the ``ignored_lines`` member.

All raw lines are kept in ``raw_lines``, which is a ``dict`` where the key is
the export path and the value is the stripped raw line.

Parsers included in this module are:

NFSExports - file ``nfs_exports``
---------------------------------

NFSExportsD - files in the ``nfs_exports.d`` directory
------------------------------------------------------

Sample content of the ``/etc/exports`` file::

    /home/utcs/shared/ro                    @group(ro,sync)   ins1.example.com(rw,sync,no_root_squash) ins2.example.com(rw,sync,no_root_squash)
    /home/insights/shared/rw                @group(rw,sync)   ins1.example.com(rw,sync,no_root_squash) ins2.example.com(ro,sync,no_root_squash)
    /home/insights/shared/special/all/mail  @group(rw,sync,no_root_squash)
    /home/insights/ins/special/all/config   @group(ro,sync,no_root_squash)  ins1.example.com(rw,sync,no_root_squash)
    #/home/insights                          ins1.example.com(rw,sync,no_root_squash)
    /home/example                           @group(rw,sync,root_squash) ins1.example.com(rw,sync,no_root_squash) ins2.example.com(rw,sync,no_root_squash)
    # A duplicate host for this exported path
    /home/example                           ins2.example.com(rw,sync,no_root_squash)

Examples:
    >>> type(exports)
    <class 'insights.parsers.nfs_exports.NFSExports'>
    >>> type(exports.data) == type({})
    True
    >>> exports.raw_lines['/home/insights/shared/rw']  # List of lines that define this path
    ['/home/insights/shared/rw                @group(rw,sync)   ins1.example.com(rw,sync,no_root_squash) ins2.example.com(ro,sync,no_root_squash)']
    >>> exports.raw_lines['/home/example']  # Lines are stored even if they contain duplicate hosts
    ['/home/example                           @group(rw,sync,root_squash) ins1.example.com(rw,sync,no_root_squash) ins2.example.com(rw,sync,no_root_squash)', '/home/example                           ins2.example.com(rw,sync,no_root_squash)']
    >>> exports.ignored_exports
    {'/home/example': {'ins2.example.com': ['rw', 'sync', 'no_root_squash']}}
    >>> sorted(list(exports.all_options()))
    ['no_root_squash', 'ro', 'root_squash', 'rw', 'sync']
    >>> sorted(list(exports.export_paths()))
    ['/home/example', '/home/insights/ins/special/all/config', '/home/insights/shared/rw', '/home/insights/shared/special/all/mail', '/home/utcs/shared/ro']