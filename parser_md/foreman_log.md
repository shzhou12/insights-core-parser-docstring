Foreman and Candlepin logs
==========================

Module for parsing the log files in foreman-debug archive

.. note::
    Please refer to its super-class :class:`insights.core.LogFileOutput` for
    usage information.

Parsers provided by this module:

CandlepinErrorLog - file ``sos_commands/foreman/foreman-debug/var/log/candlepin/error.log``
-------------------------------------------------------------------------------------------

CandlepinLog - file ``/var/log/candlepin/candlepin.log``
--------------------------------------------------------

ProductionLog - file ``/var/log/foreman/production.log``
--------------------------------------------------------

ProxyLog - file ``/var/log/foreman-proxy/proxy.log``
----------------------------------------------------

SatelliteLog - file ``/var/log/foreman-installer/satellite.log``
----------------------------------------------------------------

ForemanSSLAccessLog - file ``/var/log/httpd/foreman-ssl_access_ssl.log``
------------------------------------------------------------------------

ForemanSSLErrorLog - file ``/var/log/httpd/foreman-ssl_error_ssl.log``
----------------------------------------------------------------------