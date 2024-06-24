KatelloServiceStatus - command ``katello-service status``
=========================================================

The KatelloServiceStatus parser only reads the last line of command
``katello-service status`` to get the list of the failed services.

Note:
    Since we only care about the failed services, this parser only process the
    last line which contains the list of the failed services.

The last line of the output of ``katello-service status``::

    Some services failed to status: tomcat6,httpd


Examples:

    >>> kss_ = shared[KatelloServiceStatus]
    >>> kss.is_ok
    False
    >>> kss.failed_services
    ['tomcat6', 'httpd']