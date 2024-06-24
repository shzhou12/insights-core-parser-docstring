Cciss - Files ``/proc/driver/cciss/cciss*``
===========================================

Reads the ``/proc/driver/cciss/cciss*`` files and converts them into a
dictionary in the *data* property.

Example:
    >>> cciss = shared[Cciss]
    >>> cciss.data['Logical drives']
    '1'
    >>> 'IRQ' in cciss.data
    True
    >>> cciss.model
    'HP Smart Array P220i Controller'
    >>> cciss.firmware_version
    '3.42'