VirtWhoConf - File ``/etc/virt-who.conf`` and ``/etc/virt-who.d/*.conf``
========================================================================

The ``VirtWhoConf`` class parses the virt-who configuration files in `ini-like`
format.

    .. note::

        The configuration files under ``/etc/virt-who.d/`` might contain
        sensitive information, like ``password``. It must be filtered.