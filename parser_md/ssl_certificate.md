Get SSL Certificate Info
========================

This module contains the following parsers:

SatelliteCustomCaChain - command ``awk 'BEGIN { pipe="openssl x509 -noout -subject -enddate"} /^-+BEGIN CERT/,/^-+END CERT/ { print | pipe } /^-+END CERT/ { close(pipe); printf("\n")}' /etc/pki/katello/certs/katello-server-ca.crt``
========================================================================================================================================================================================================================================
RhsmKatelloDefaultCACert - command ``openssl x509 -in /etc/rhsm/ca/katello-default-ca.pem -noout -issuer``
==========================================================================================================
HttpdSSLCertExpireDate - command ``openssl x509 -in httpd_certificate_path -enddate -noout``
============================================================================================
NginxSSLCertExpireDate - command ``openssl x509 -in nginx_certificate_path -enddate -noout``
============================================================================================
MssqlTLSCertExpireDate - command ``openssl x509 -in mssql_tls_cert_file -enddate -noout``
============================================================================================
HttpdCertInfoInNSS - command ``certutil -L -d xxx -n xxx``
==========================================================