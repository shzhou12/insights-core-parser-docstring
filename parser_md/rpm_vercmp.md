Nearly direct translation of rpm comparison code in the rpm project at
https://github.com/rpm-software-management/rpm/blob/master/lib/rpmvercmp.c

Handles all of the cases in the rpm test file, including the "buggy" tests
and non-ascii characters.

https://raw.githubusercontent.com/rpm-software-management/rpm/master/tests/rpmvercmp.at