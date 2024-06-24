Scheduler - file ``/sys/block/*/queue/scheduler``
=================================================

This parser parses the content from scheduler files. It stores available
values and also current selection for every device.

Sample content from schduler file:

    noop deadline [cfq]

Examples:
    >>> type(scheduler_obj)
    <class 'insights.parsers.scheduler.Scheduler'>
    >>> scheduler_obj.data
    {'sda': '[cfq]'}
    >>> scheduler_obj.device
    'sda'
    >>> scheduler_obj.schedulers
    ['noop', 'deadline', 'cfq']
    >>> scheduler_obj.active_scheduler
    'cfq'