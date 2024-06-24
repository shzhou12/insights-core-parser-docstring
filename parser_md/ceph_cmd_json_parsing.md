Ceph status commands
====================

This module provides processing for the output of the following ceph related
commands with ``-f json-pretty`` parameter.

CephOsdDump - command ``ceph osd dump -f json-pretty``
------------------------------------------------------

CephOsdDf - command ``ceph osd df -f json-pretty``
--------------------------------------------------

CephS - command ``ceph -s -f json-pretty``
------------------------------------------

CephDfDetail - command ``ceph df detail -f json-pretty``
--------------------------------------------------------

CephHealthDetail - command ``ceph health detail -f json-pretty``
--------------------------------------------------------------------------

CephECProfileGet - command ``ceph osd erasure-code-profile get default -f json-pretty``
---------------------------------------------------------------------------------------

CephCfgInfo - command ``ceph daemon {ceph_socket_files} config show``
---------------------------------------------------------------------

CephOsdTree - command ``ceph osd tree -f json-pretty``
------------------------------------------------------

CephReport - command ``ceph report``
------------------------------------

All these parsers are based on a shared class which processes the JSON
information into a dictionary.