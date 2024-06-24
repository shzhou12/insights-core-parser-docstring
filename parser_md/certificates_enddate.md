CertificatesEnddate - command ``/usr/bin/openssl x509 -noout -enddate -in path/to/cert/file``
=============================================================================================

This command gets the enddate of the certificate files.

Sample Output::

    /usr/bin/find: '/etc/origin/node': No such file or directory
    /usr/bin/find: '/etc/origin/master': No such file or directory
    notAfter=May 25 16:39:40 2019 GMT
    FileName= /etc/origin/node/cert.pem
    unable to load certificate
    139881193203616:error:0906D066:PEM routines:PEM_read_bio:bad end line:pem_lib.c:802:
    unable to load certificate
    140695459370912:error:0906D06C:PEM routines:PEM_read_bio:no start line:pem_lib.c:703:Expecting: TRUSTED CERTIFICATE
    notAfter=May 25 16:39:40 2019 GMT
    FileName= /etc/pki/ca-trust/extracted/pem/email-ca-bundle.pem
    notAfter=Dec  9 10:55:38 2017 GMT
    FileName= /etc/pki/consumer/cert.pem
    notAfter=Jan  1 04:59:59 2022 GMT
    FileName= /etc/pki/entitlement/3343502840335059594.pem
    notAfter=Aug 31 02:19:59 2017 GMT
    FileName= /etc/pki/consumer/cert.pem
    notAfter=Jan  1 04:59:59 2022 GMT
    FileName= /etc/pki/entitlement/2387590574974617178.pem

Examples:
    >>> type(cert_enddate)
    <class 'insights.parsers.certificates_enddate.CertificatesEnddate'>
    >>> paths = cert_enddate.certificates_path
    >>> '/etc/origin/node/cert.pem' in paths
    True
    >>> cert_enddate.expiration_date('/etc/origin/node/cert.pem').datetime
    datetime.datetime(2019, 5, 25, 16, 39, 40)
    >>> cert_enddate.expiration_date('/etc/origin/node/cert.pem').str
    'May 25 16:39:40 2019'