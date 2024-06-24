QPID statistics - command ``qpid-stat``
=======================================

This module contains parsers that check the QPID daemon statistics.  qpidd is
used by Satellite for communication between clients, capsules and servers.

Parsers provided by this module are:

QpidStatQ - command ``/usr/bin/qpid-stat -q --ssl-certificate=/etc/pki/katello/qpid_client_striped.crt -b amqps://localhost:5671``
----------------------------------------------------------------------------------------------------------------------------------

QpidStatU - command ``/usr/bin/qpid-stat -u --ssl-certificate=/etc/pki/katello/qpid_client_striped.crt -b amqps://localhost:5671``
----------------------------------------------------------------------------------------------------------------------------------

QpidStatG - command ``/usr/bin/qpid-stat -g --ssl-certificate=/etc/pki/katello/qpid_client_striped.crt -b amqps://localhost:5671``
----------------------------------------------------------------------------------------------------------------------------------