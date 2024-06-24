Modprobe configuration - files ``/etc/modprobe.conf`` and ``/etc/modprobe.d/*.conf``
====================================================================================

This parser collects command information from the Modprobe configuration
files and stores information about each module mentioned. Lines such as
comments and those without the commands 'alias', 'blacklist', 'install',
'options', 'remove' and 'softdep' are ignored.

Blacklisted modules simply have True as their value in the dictionary.  Alias
lines list the module last, and these are recorded as a list of aliases.  For
all other commands the module name (after the command) is used as the key,
and the rest of the line is split up and stored as a list.  Any lines that
don't parse, either because they're not long enough or because they don't
start with a valid keyword, are stored in the ``bad_lines`` property list.

Sample file ``/etc/modprobe.conf``::

    alias scsi_hostadapter2 qla2xxx
    alias scsi_hostadapter3 usb-storage
    alias net-pf-10 off
    alias ipv6 off
    alias bond0 bonding
    alias bond1 bonding
    options bonding max_bonds=2
    options bnx2 disable_msi=1

Examples:

    >>> mconf_list = shared[ModProbe] # A list: multiple files may be found
    >>> for mconf in mconf_list:
    ...     print "File:", mconf.file_name
    ...     print "Modules with aliases:", sorted(mconf.data['alias'].keys())
    File: /etc/modprobe.conf
    Modules with aliases: ['bonding', 'off', 'qla2xxx', 'usb-storage']