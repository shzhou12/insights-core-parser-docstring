InitProcessCgroup - File ``/proc/1/cgroup``
===========================================

This parser reads the content of ``/proc/1/cgroup``.
This file shows the cgroup detail of init process.
The format of the content is like key-value. We can
also use this info to check if the archive is from
container or host.