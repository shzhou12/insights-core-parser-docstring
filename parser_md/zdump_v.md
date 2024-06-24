ZdumpV - command ``/usr/sbin/zdump -v /etc/localtime -c 2019,2039``
===================================================================

The ``/usr/sbin/zdump -v /etc/localtime -c 2019,2039`` command provides information about
'Daylight Saving Time' in file /etc/localtime from 2019 to 2039.

Sample content from command ``zdump -v /etc/localtime -c 2019,2039`` is::

    /etc/localtime  Sun Mar 10 06:59:59 2019 UTC = Sun Mar 10 01:59:59 2019 EST isdst=0 gmtoff=-18000
    /etc/localtime  Sun Mar 10 07:00:00 2019 UTC = Sun Mar 10 03:00:00 2019 EDT isdst=1 gmtoff=-14400
    /etc/localtime  Sun Nov  7 05:59:59 2038 UTC = Sun Nov  7 01:59:59 2038 EDT isdst=1 gmtoff=-14400
    /etc/localtime  Sun Nov  7 06:00:00 2038 UTC = Sun Nov  7 01:00:00 2038 EST isdst=0 gmtoff=-18000

Examples:
    >>> dst = zdump[0]
    >>> dst.get('utc_time')
    datetime.datetime(2019, 3, 10, 6, 59, 59)
    >>> dst.get('utc_time_raw')
    'Sun Mar 10 06:59:59 2019 UTC'
    >>> dst.get('local_time')
    datetime.datetime(2019, 3, 10, 1, 59, 59)
    >>> dst.get('local_time_raw')
    'Sun Mar 10 01:59:59 2019 EST'
    >>> dst.get('isdst')
    0
    >>> dst.get('gmtoff')
    -18000