HammerPing - command ``/usr/bin/hammer ping``
=============================================

The hammer ping parser reads the output of ``hammer ping`` and turns it into
a dictionary. The key is the service name, and the value is a dict of all the
service info.

Sample output of ``hammer ping``::

    candlepin:
        Status:          FAIL
        Server Response: Message: 404 Resource Not Found
    elasticsearch:
        Status:          ok
        Server Response: Duration: 35ms
    foreman_tasks:
        Status:          ok
        Server Response: Duration: 1ms

Examples:

    >>> type(hammer_ping)
    <class 'insights.parsers.hammer_ping.HammerPing'>
    >>> 'unknown_service' in hammer_ping.service_list
    False
    >>> hammer_ping['candlepin']['Status']
    'FAIL'
    >>> hammer_ping['candlepin']['Server Response']
    'Message: 404 Resource Not Found'
    >>> hammer_ping.are_all_ok
    False
    >>> hammer_ping.services_of_status('OK')
    ['elasticsearch', 'foreman_tasks']