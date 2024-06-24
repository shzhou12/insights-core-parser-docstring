FCMatch - command ``/bin/fc-match -sv 'sans:regular:roman' family fontformat``
==============================================================================

This command gets the fonts information in the current system.

Typical output of this command is::

    Pattern has 2 elts (size 16)
        family: "DejaVu Sans"(s)
        fontformat: "TrueType"(w)

    Pattern has 2 elts (size 16)
        family: "DejaVu Sans"(s)
        fontformat: "TrueType"(w)

    Pattern has 2 elts (size 16)
        family: "DejaVu Sans"(s)
        fontformat: "TrueType"(w)

    Pattern has 2 elts (size 16)
        family: "Nimbus Sans L"(s)
        fontformat: "Type 1"(s)

    Pattern has 2 elts (size 16)
        family: "Standard Symbols L"(s)
        fontformat: "Type 1"(s)

.. note::
    As there is a bug on RHEL6 that can cause segfault when executing ``fc-match`` command, we only parse the command output on RHEL7 before the bug is fixed.

Examples:
    >>> fc_match = shared[FCMatch]
    >>> fc_match_info = fc_match[0]
    >>> fc_match_info
    {'fontformat': '"TrueType"(w)', 'family': '"DejaVu Sans"(s)'}