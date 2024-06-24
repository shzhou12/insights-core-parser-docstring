InitScript - files ``/etc/rc.d/init.d/*``
=========================================

InitScript is a parser for the initscripts in ``/etc/rc.d/init.d``.

Because this parser read multiple files, the initscripts are stored as a list
within the parser and need to be iterated through in order to find specific
initscripts.

Examples:

    >>> for initscript in shared[InitScript]: # Parser contains list of all initscripts
    ...     print "Name:", initscript.file_name
    ...
    Name: netconsole
    Name: rhnsd