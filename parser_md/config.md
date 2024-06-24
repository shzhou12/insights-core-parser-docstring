SystemD service configuration
=============================

Service systemd files are in ``/usr/lib/systemd/system/`` or ``/etc/systemd/``,
and their content format is similar to a '.ini' file.

Parsers included in this module are:

SystemdDocker - file ``/usr/lib/systemd/system/docker.service``
---------------------------------------------------------------

SystemdLogindConf - file ``/etc/systemd/logind.conf``
-----------------------------------------------------

SystemdRpcbindSocketConf - unit file ``rpcbind.socket``
-------------------------------------------------------

SystemdDnsmasqServiceConf - unit file ``dnsmasq.service``
---------------------------------------------------------

SystemdOpenshiftNode - file ``/usr/lib/systemd/system/atomic-openshift-node.service``
-------------------------------------------------------------------------------------

SystemdSystemConf - file ``/etc/systemd/system.conf``
-----------------------------------------------------

SystemdOriginAccounting - file ``/etc/systemd/system.conf.d/origin-accounting.conf``
------------------------------------------------------------------------------------