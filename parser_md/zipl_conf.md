ZiplConf - configuration file for zipl
======================================

A parser file for parsing and extracting data from ``/etc/zipl.conf`` file.

Sample input::

    [defaultboot]
    defaultauto
    prompt=1
    timeout=5
    default=linux
    target=/boot
    [linux]
        image=/boot/vmlinuz-3.10.0-693.el7.s390x
        ramdisk=/boot/initramfs-3.10.0-693.el7.s390x.img
        parameters="root=/dev/mapper/rhel_gss5-root crashkernel=auto rd.dasd=0.0.0100 rd.dasd=0.0.0101 rd.dasd=0.0.0102 rd.lvm.lv=rhel_gss5/root rd.lvm.lv=rhel_gss5/swap net.ifnames=0 rd.znet=qeth,0.0.0600,0.0.0601,0.0.0602,layer2=0,portname=gss5,portno=0 LANG=en_US.UTF-8"
    [linux-0-rescue-a27932c8d57248e390cee3798bbd3709]
        image=/boot/vmlinuz-0-rescue-a27932c8d57248e390cee3798bbd3709
        ramdisk=/boot/initramfs-0-rescue-a27932c8d57248e390cee3798bbd3709.img
        parameters="root=/dev/mapper/rhel_gss5-root crashkernel=auto rd.dasd=0.0.0100 rd.dasd=0.0.0101 rd.dasd=0.0.0102 rd.lvm.lv=rhel_gss5/root rd.lvm.lv=rhel_gss5/swap net.ifnames=0 rd.znet=qeth,0.0.0600,0.0.0601,0.0.0602,layer2=0,portname=gss5,portno=0"
    # Configuration for dumping to SCSI disk
    # Separate IPL and dump partitions
    [dumpscsi]
    target=/boot
    dumptofs=/dev/sda2
    parameters="dump_dir=/mydumps dump_compress=none dump_mode=auto"
    # Menu containing two DASD boot configurations
    :menu1
    1=linux
    2=linux-0-rescue-a27932c8d57248e390cee3798bbd3709
    default=1
    prompt=1
    timeout=30

This module contains one parser:

ZiplConf - file ``/etc/zipl.conf``
----------------------------------

Examples:
    >>> zipl_info['linux']['image']
    '/boot/vmlinuz-3.10.0-693.el7.s390x'
    >>> zipl_info.images
    {'linux':'/boot/vmlinuz-3.10.0-693.el7.s390x','linux-0-rescue-a27932c8d57248e390cee3798bbd3709':'/boot/vmlinuz-0-rescue-a27932c8d57248e390cee3798bbd3709'}
    >>> zipl_info.dumptofses
    {'dumpscsi':'/dev/sda2'}
    >>> zipl_info[':menu1']['1']
    'linux'
    >>> 'defaultauto' in zipl_info['global']
    True
    >>> zipl_info['global']['defaultauto']
    None