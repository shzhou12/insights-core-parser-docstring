MultipathDevices - command ``multipath -v4 -ll``
================================================

This function converts the output of the ``multipath -v4 -ll`` command and
stores the data around each multipath device given.

Examples:
    >>> type(mpaths)
    <class 'insights.parsers.multipath_v4_ll.MultipathDevices'>
    >>> len(mpaths)  # Can treat the object as a list to iterate through
    3
    >>> mpaths[0]['alias']
    'mpathg'
    >>> mpaths[0]['size']
    '54T'
    >>> mpaths[0]['dm_name']
    'dm-2'
    >>> mpaths[0]['wwid']
    '36f01faf000da360b0000033c528fea6d'
    >>> groups = mpaths[0]['path_group']  # List of path groups for this device
    >>> groups[0]['status']
    'active'
    >>> len(groups[0]['path'])
    4
    >>> path0 = groups[0]['path'][0]  # Each path group has an array of paths
    >>> path0[1]  # Paths are stored as a list of items
    'sdc'
    >>> path0[-1]
    'running'
    >>> mpaths.dms  # List of device names found
    ['dm-2', 'dm-4', 'dm-5']
    >>> mpaths.by_dm['dm-2']['alias']  # Access by device name
    'mpathg'
    >>> mpaths.aliases  # Aliases found (again, in order)
    ['mpathg', 'mpathe']
    >>> mpaths.by_alias['mpathg']['dm_name']  # Access by alias
    'dm-2'
    >>> mpaths.by_wwid['36f01faf000da360b0000033c528fea6d']['dm_name']
    'dm-2'