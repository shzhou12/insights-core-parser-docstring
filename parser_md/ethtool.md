Ethtool parsers
===============

Classes to parse ``ethtool`` command information.

The interface information for a machine is stored as lists.  Each interface
is accessed by iterating through the shared parser list.

The interface classes all provide the following properties:

* ``iface`` and ``ifname``: the interface name (derived from the output file).
* ``data``: the data for that interface

Parsers provided by this module include:

CoalescingInfo - command ``/sbin/ethtool -c {interface}``
---------------------------------------------------------

Driver - command ``/sbin/ethtool -i {interface}``
-------------------------------------------------

Ethtool - command ``/sbin/ethtool {interface}``
-----------------------------------------------

Features - command ``/sbin/ethtool -k {interface}``
---------------------------------------------------

Pause - command ``/sbin/ethtool -a {interface}``
------------------------------------------------

Ring - command ``/sbin/ethtool -g {interface}``
-----------------------------------------------

Statistics - command ``/sbin/ethtool -S {interface}``
-----------------------------------------------------

TimeStamp - command ``/sbin/ethtool -T {interface}``
----------------------------------------------------