Lsof - command ``/usr/sbin/lsof``
=================================

This parser reads the output of the ``/usr/sbin/lsof`` command and makes each
line available as a dictionary keyed on the fields in the lsof output (with
names in upper case).

Because of the large quantity of output from this command, this class is based
on the ``Scannable`` parser class.  There are several ways to use this:

* If you simply want to know whether a search matched, use the ``any`` method.
* If you want all lines that match, use the ``collect`` method.

The way these scanner functions work is:

1. You provide a function, which returns True if a match is found, and an
   attribute name.
2. The parser runs every scanner function across every line of data read and
   successfully parsed.
3. The attribute then contains the result of the match (True or False in the
   case of the ``any`` method, or the list of matching rows in the case of
   the ``collect`` method.

As an easier way of finding all the lines that match by key=value pairs, use
the ``collect_keys`` method, giving the name of the scanner attribute to set
and one or more 'key=value' pairs in the method call.  This then returns the
list of rows for which the data in all those keywords matched the respective
given values.  (**Note**: the ``SIZE/OFF`` column is searched for using the
key ``SIZE_OFF`` - see example below)

Sample output::

    COMMAND     PID  TID           USER   FD      TYPE             DEVICE  SIZE/OFF       NODE NAME
    systemd       1                root  cwd       DIR              253,1      4096        128 /
    systemd       1                root  rtd       DIR              253,1      4096        128 /
    systemd       1                root  txt       REG              253,1   1230920    1440410 /usr/lib/systemd/systemd
    systemd       1                root  mem       REG              253,1     37152  135529970 /usr/lib64/libnss_sss.so.2
    abrt-watc  8619                root    0r      CHR                1,3       0t0       4674 /dev/null
    wpa_suppl   641                root    0r      CHR                1,3       0t0       4674 /dev/null
    polkitd     642             polkitd    0u      CHR                1,3       0t0       4674 /dev/null
    polkitd     642             polkitd    1u      CHR                1,3       0t0       4674 /dev/null

Examples:

    >>> Lsof.any('systemd_commands', lambda x: 'systemd' in x['COMMAND'])
    >>> Lsof.collect('polkitd_user', lambda x: x['USER'] == 'polkitd')
    >>> Lsof.collect_keys('root_stdin', USER='root', FD='0r', SIZE_OFF='0t0')
    >>> l = shared[Lsof]
    >>> l.systemd_commands
    True
    >>> len(l.polkitd_user)
    2
    >>> l.polkitd_user[0]['DEVICE']
    '1,3'
    >>> len(l.root_stdin)
    2
    >>> l.root_stdin[0]['COMMAND']
    'abrt-watc'