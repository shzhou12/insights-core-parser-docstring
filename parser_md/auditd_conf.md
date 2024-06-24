Audit Conf files parsers
========================

The auditd.conf file is a standard key = value file with hash comments.
Active settings are provided using the `get_active_settings_value` method or
by using the dictionary `contains` functionality.

The audispd.conf file has the same format and usage with auditd.conf.

.. note::
    For Red Hat Enterprise Linux 7 and older, auditd and audispd are separate
    processes.
    Starting with Red Hat Enterprise Linux 8 the functionality of audispd has
    been migrated to auditd.

AuditdConf - file ``/etc/audit/auditd.conf``
--------------------------------------------

AudispdConf - file ``/etc/audisp/audispd.conf``
-----------------------------------------------

Example:

    >>> conf = shared[AuditdConf]
    >>> conf.get_active_setting_value('log_group')
    'root'
    >>> 'log_file' in conf
    True