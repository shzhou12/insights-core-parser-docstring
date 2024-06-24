Dcbtool - Command ``/sbin/dcbtool gc {interface} dcb``
======================================================

    Parse Lines from the `dcbtool gc eth1 dcb` to check DCBX if enabled

    Successful completion of the command returns data similar to::

        Command:    Get Config
        Feature:    DCB State
        Port:       eth0
        Status:     Off
        DCBX Version: FORCED CIN

    The keys in this data are converted to lower case and spaces are converted
    to underscores.

    An `is_on` attribute is also provided to indicate if the status is 'On'.

    Examples:

        >>> dcbstate = shared[Dcbtool]
        >>> dcb.data
        {
            "command": "Get Config",
            "feature": "DCB State",
            "port": "eth0",
            "status": "Off"
            "dcbx_version":"FORCED CIN"
        }
        >>> dcb['port']
        'eth0'
        >>> dcb['state']
        'Off'
        >>> dcb.is_on
        False

    If a "Connection refused" error is encountered,
    an empty dictionary is returned`.