SatelliteContentHostsCount - command ``psql -d foreman -c 'select count(*) from hosts'``
========================================================================================

The SatelliteContentHostsCount parser reads the output of
``psql -d foreman -c 'select count(*) from hosts'``.

Sample output of ``psql -d foreman -c 'select count(*) from hosts'``::

     count
    -------
        13
    (1 row)

Examples::

    >>> type(clients)
    <class 'insights.parsers.satellite_content_hosts_count.SatelliteContentHostsCount'>
    >>> clients.count
    13