PostgreSQLConf - file ``/var/lib/pgsql/data/postgresql.conf``
=============================================================

The PostgreSQL configuration file is in a fairly standard 'key = value'
format, with the equals sign being optional.  A hash mark (#) marks the
rest of the line as a comment.

The configuration then appears as a dictionary in the `data` property.

This parser does not attempt to know the default value of any property; it
only shows what's defined in the configuration file as given.

This parser also provides several utility functions to make sense of values
specific to PostgreSQL.  These are:

  * `as_duration(property)`
      Convert the value (given in milliseconds, seconds, minutes, hours or
      days) to seconds (as a floating point value).
  * `as_boolean(property)`
      If the value is 'on', 'true', 'yes', or '1', return True.  If the value
      is 'off', 'false', 'no' or '0', return False.  Unique prefixes of these
      are acceptable and case is ignored.
  * `as_memory_bytes(property)`
      Convert a number given in KB, MB or GB into bytes, where 1 kilobyte is
      1024 bytes.

All three type conversion functions will raise a ValueError if the value
doesn't match the spec or cannot be converted to the correct type.

Example:
    >>> pgsql = shared[PostgreSQLConf]
    >>> 'port' in pgsql
    True
    >>> pgsql['port']
    '5432'
    >>>