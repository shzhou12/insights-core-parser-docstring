Satellite6Version - file ``/usr/share/foreman/lib/satellite/version.rb``
========================================================================

Module for parsing the content of file ``version.rb`` or ``satellite_version``,
which is a simple file in foreman-debug or sosreport archives of Satellite 6.x.

Typical content of "satellite_version" is::

    COMMAND> cat /usr/share/foreman/lib/satellite/version.rb

    module Satellite
      VERSION = "6.1.3"
    end

.. warning::
    This module only works for Satellite 6.0.x and 6.1.x
    Please use the combiner
    :class:`insights.combiners.satellite_version.SatelliteVersion` class to
    cover all versions.

Examples:
    >>> sat6_ver = shared[SatelliteVersion]
    >>> sat6_ver.full
    "6.1.3"
    >>> sat6_ver.version
    "6.1.3"
    >>> sat6_ver.major
    6
    >>> sat6_ver.minor
    1
    >>> sat6_ver.release
    None