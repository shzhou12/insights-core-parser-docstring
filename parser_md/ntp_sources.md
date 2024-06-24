NTP sources - remote clock info from ``ntpq`` and ``chronyc``
=============================================================

The parsers here provide information about the time sources used by
``ntpd`` and ``chronyd``.  These are gathered from the output of the
``ntpq -pn`` and ``chronyc sources`` commands respectively.

There is also a parser for parsing the output of ``ntpq -c 'rv 0 leap'``
command to give leap second status.

Parsers in this module are:

ChronycSources - command ``/usr/bin/chronyc sources``
-----------------------------------------------------

NtpqPn - command ``/usr/sbin/ntpq -pn``
---------------------------------------

NtpqLeap - command ``/usr/sbin/ntpq -c 'rv 0 leap'``
----------------------------------------------------