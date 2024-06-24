PuppetCertExpireDate - command ``openssl x509 -in /etc/puppetlabs/puppet/ssl/ca/ca_crt.pem -enddate -noout``
============================================================================================================

The PuppetCertExpireDate parser reads the output of
``openssl x509 -in /etc/puppetlabs/puppet/ssl/ca/ca_crt.pem -enddate -noout``.

Sample output of ``openssl x509 -in /etc/puppetlabs/puppet/ssl/ca/ca_crt.pem -enddate -noout``::

    notAfter=Dec  4 07:04:05 2035 GMT

Examples::

    >>> type(date_info)
    <class 'insights.parsers.puppet_ca_cert_expire_date.PuppetCertExpireDate'>
    >>> date_info['notAfter'].datetime
    datetime.datetime(2035, 12, 4, 7, 4, 5)