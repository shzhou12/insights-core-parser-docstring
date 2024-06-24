HttpdV - command ``httpd -V``
=============================

Module for parsing the output of command ``httpd -V``.   The bulk of the
content is split on the colon and keys are kept as is.  Lines beginning with
'-D' are kept in a dictionary keyed under 'Server compiled with'; each
compilation option is a key in this sub-dictionary.  The value of the
compilation options is the value after the equals sign, if one is present,
or the value in brackets after the compilation option, or 'True' if only the
compilation option is present.