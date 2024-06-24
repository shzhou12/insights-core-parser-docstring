Journald configuration files
============================

The journald.conf file is a key=value file with hash comments. Everything is in the [Journal]
section, so sections are ignored.

Only active settings lines are processed, commented out settings are not processed.

Active settings are provided using the `get_active_settings_value` method or
by using the dictionary `contains` functionality.

Options that are commented out are not returned - a rule using this parser has to be aware of which
default value is assumed by systemd if the particular option is not specified.

Note: Precedence logic is implemented in JournaldConfAll combiner, the parser is called for every
file separately.

Parsers provided by this module are:

EtcJournaldConf - file ``/etc/systemd/journald.conf``
-----------------------------------------------------

EtcJournaldConfD - file ``/etc/systemd/journald.conf.d/*.conf``
---------------------------------------------------------------

UsrJournaldConfD - file ``usr/lib/systemd/journald.conf.d/*.conf``
------------------------------------------------------------------

Example:

    >>> conf = shared[EtcJournaldConf]
    >>> conf.get_active_setting_value('Storage')
    'auto'
    >>> 'Storage' in conf.active_settings
    True