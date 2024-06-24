NumericUserGroupName - command ``/usr/bin/grep -c '^[[:digit:]]' /etc/passwd /etc/group``
=========================================================================================

This parser reads the output of ``/usr/bin/grep -c '^[[:digit:]]' /etc/passwd /etc/group``
and detects whether there are any user or group names that begin with a digit.

The grep command returns the number of matches for each file. It matches for user and
group names that begin with a number.

The answers are available through attributes - boolean ``has_numeric_user_group`` and
numeric ``nr_numeric_user`` and ``nr_numeric_group``.

Names starting with a digit can be handled incorrectly by some software. Purely numeric
user names can be handled incorrectly by some software and requires special care when
used with utilities that accept both user/group IDs and names (like chown, chmod). In
case such names exist on the system, it is advisable to review whether the used software
(namely 3rd party software and shell scripts) handles the names correctly.

https://access.redhat.com/solutions/3103631

Sample input::

    /etc/passwd:3
    /etc/group:0

Examples:

    >>> shared[NumericUserGroupName].has_numeric_user_or_group
    True
    >>> shared[NumericUserGroupName].nr_numeric_user
    3
    >>> shared[NumericUserGroupName].nr_numeric_group
    0