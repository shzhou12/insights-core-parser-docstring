Facter - command ``/usr/bin/facter``
====================================

Module for the parsing of output from the ``facter`` command.
Data is avaliable as a dict for each line of the output.

Sample input data for the ``facter`` command looks like::

    architecture => x86_64
    bios_vendor => Phoenix Technologies LTD
    bios_version => 6.00
    domain => example.com
    facterversion => 1.7.6
    filesystems => btrfs,ext2,ext3,ext4,msdos,vfat,xfs
    fqdn => plin-w1rhns01.example.com
    hostname => plin-w1rhns01
    ipaddress => 172.23.27.50
    ipaddress_ens192 => 172.23.27.50
    ipaddress_lo => 127.0.0.1
    is_virtual => true
    kernel => Linux
    kernelmajversion => 3.10

Examples:
    >>> facts_info = shared[facter]
    >>> facts_info.kernelmajversion
    '3.10'
    >>> facts_info.domain
    'example.com'
    >>> facts_info.architecture
    'x86_64'