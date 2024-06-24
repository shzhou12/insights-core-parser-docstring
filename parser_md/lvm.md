Logical Volume Management configuration and status
==================================================

Parsers for lvm data based on output of various commands and file contents.

This module contains the classes that parse the output of the commands `lvs`,
`pvs`, and `vgs`, and the content of the files `/etc/lvm/lvm.conf`,
`/etc/lvm/devices/system.devices`.

Pvs - command ``/sbin/pvs --nameprefixes --noheadings --separator='|' -a -o pv_all``
------------------------------------------------------------------------------------

PvsHeadings - command ``pvs -a -v -o +pv_mda_free,pv_mda_size,pv_mda_count,pv_mda_used_count,pe_count --config="global{locking_type=0}"``
-----------------------------------------------------------------------------------------------------------------------------------------

Vgs - command ``/sbin/vgs --nameprefixes --noheadings --separator='|' -a -o vg_all``
------------------------------------------------------------------------------------

VgsHeadings - command ``vgs -v -o +vg_mda_count,vg_mda_free,vg_mda_size,vg_mda_used_count,vg_tags --config="global{locking_type=0}"``
-------------------------------------------------------------------------------------------------------------------------------------

Lvs - command ``/sbin/lvs --nameprefixes --noheadings --separator='|' -a -o lv_name,lv_size,lv_attr,mirror_log,vg_name,devices,region_size,data_percent,metadata_percent,segtype,seg_monitor --config="global{locking_type=0}"``
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

LvsHeadings - command ``/sbin/lvs -a -o +lv_tags,devices --config="global{locking_type=0}"``
--------------------------------------------------------------------------------------------

LvmConf - file ``/etc/lvm/lvm.conf``
------------------------------------

LvmSystemDevices - file ``/etc/lvm/devices/system.devices``
-----------------------------------------------------------

LvmFullReport - command ``/sbin/lvm fullreport -a --reportformat json``
-----------------------------------------------------------------------