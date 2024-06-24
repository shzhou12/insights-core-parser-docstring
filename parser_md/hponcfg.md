HponConf - command ``/sbin/hponcfg -g``
=======================================

Get the iLO firmware revision from the ``hponcfg`` command.
This is a 3rd party utility from HP and isn't shipped with RHEL.  However,
it's useful for detecting possible hardware incompatibilities.

There are only five pieces of information extracted:

* **firmware_revision** - the ``Firmware Revision`` value
* **device_type** - the ``Device type`` value
* **driver_name** - the ``Driver name`` value
* **server_name** - the ``Server Name`` value
* **server_number** - the ``Server Number`` value

Values are '' if not listed in the output.

Input looks like this::

    HP Lights-Out Online Configuration utility
    Version 4.3.1 Date 05/02/2014 (c) Hewlett-Packard Company, 2014
    Firmware Revision = 1.22 Device type = iLO 4 Driver name = hpilo
    Host Information:
                            Server Name: esxi01.hp.local
                            Server Number:

Examples:

    >>> cfg = shared[HponConf]
    >>> cfg.data['firmware_revision']
    '1.22'
    >>> cfg.data['server_name']
    'esxi01.hp.local'
    >>> cfg.data['server_number']
    ''
    >>> 'Version' in cfg.data # other values in the hponcfg output not found
    False