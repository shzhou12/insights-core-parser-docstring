transparent_hugepage sysfs settings
===================================

Module for parsing the sysfs settings for transparent_hugepage:

ThpUseZeroPage - file ``/sys/kernel/mm/transparent_hugepage/use_zero_page``
---------------------------------------------------------------------------

Gets the contents of /sys/kernel/mm/transparent_hugepage/use_zero_page, which is either 0 or 1.

Sample input::

    0

Examples:

    >>> shared[ThpUseZeroPage].use_zero_page
    0


ThpEnabled - file ``/sys/kernel/mm/transparent_hugepage/enabled``
-----------------------------------------------------------------

Gets the contents of  /sys/kernel/mm/transparent_hugepage/enabled, which is something like
`always [madvise] never` where the active value is in brackets.

If no option is active (that should never happen), `active_option` will contain None.

Sample input::

    always [madvise] never

Examples:

    >>> shared[ThpEnabled].line
    always [madvise] never
    >>> shared[ThpEnabled].active_option
    madvise