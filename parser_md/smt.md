Simultaneous Multithreading (SMT) parsers
=========================================

Parsers included in this module are:

CpuSMTActive - file ``/sys/devices/system/cpu/smt/active``
----------------------------------------------------------
CpuSMTControl - file ``/sys/devices/system/cpu/smt/control``
------------------------------------------------------------
CpuCoreOnline - files matching ``/sys/devices/system/cpu/cpu[0-9]*/online``
---------------------------------------------------------------------------
CpuSiblings - files matching ``/sys/devices/system/cpu/cpu[0-9]*/topology/thread_siblings_list``
------------------------------------------------------------------------------------------------