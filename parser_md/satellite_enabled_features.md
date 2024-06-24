SatelliteEnabledFeatures - command ``curl -sk https://localhost:9090/features --connect-timeout 5``
===================================================================================================

The satellite enabled features parser reads the output of
``curl -sk https://localhost:9090/features --connect-timeout 5`` and convert it into a list.

Sample output of ``curl -sk https://localhost:9090/features --connect-timeout 5``::

    ["ansible","dhcp","discovery",dynflow","logs","openscap","pulp","puppet","puppetca","ssh","templates","tftp"]

Examples:

    >>> type(satellite_features)
    <class 'insights.parsers.satellite_enabled_features.SatelliteEnabledFeatures'>
    >>> 'dhcp' in satellite_features
    True
    >>> 'dns' in satellite_features
    False