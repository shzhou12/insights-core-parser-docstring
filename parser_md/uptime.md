Uptime - command ``/usr/bin/uptime``
====================================

Parse the output of the ``uptime`` command into six attributes:

* ``currtime``: the time on the system as a string.
* ``loadavg``: a three element array of strings for the one, five and
  fifteen minute load averages.
* ``updays``: a string of the number of days the system has been up, or ''
  if the system has been running for less than a day.
* ``uphhmm``: a string of the fraction of a day in hours and minutes that the
  system has been running.  Times reported by ``uptime`` as e.g. '30 mins' are
  converted in to hh:mm format.
* ``users``: a string containing the number of users ``uptime`` reports as
  using the system.
* ``uptime``: a ``datetime.timedelta`` object of the total duration of uptime.

These can also be queried as named keys in the ``data`` attribute.

Sample output::

     11:51:06 up  3:17,  1 user,  load average: 0.12, 0.20, 0.28

Examples:
    >>> uptime = shared[Uptime]
    >>> from datetime import timedelta
    >>> uptime.uptime > timedelta(days=1)
    False
    >>> uptime.updays
    ''
    >>> uptime.users
    '1'
    >>> uptime.loadavg[1]
    '0.20'
    >>> uptime.data['currtime']
    '11:51:06'