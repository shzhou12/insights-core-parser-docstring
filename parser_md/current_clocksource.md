CurrentClockSource - file ``/sys/devices/system/clocksource/clocksource0/current_clocksource``
==============================================================================================

This is a relatively simple parser that reads the
``/sys/devices/system/clocksource/clocksource0/current_clocksource`` file.
As well as reporting the contents of the file in its ``data`` property, it
also provides three properties that are true if the clock source is set to
that value:

    * **is_kvm** - the clock source file contains 'kvm-clock'
    * **is_tsc** - the clock source file contains 'tsc'
    * **is_vmi_timer** - the clock source file contains 'vmi-timer'

Examples:

    >>> cs = shared[CurrentClockSource]
    >>> cs.data
    'tsc'
    >>> cs.is_tsc
    True