MaxUID - command ``/bin/awk -F':' '{ if($3 > max) max = $3 } END { print max }' /etc/passwd``
=============================================================================================

This module provides the MaxUID value gathered from the ``/etc/passwd`` file.