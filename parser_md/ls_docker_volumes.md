DockerVolumesDir - command ``ls -lanR /var/lib/docker/volumes/``
================================================================

A standard directory listing parser using the FileListing parser class.

Given a listing of::

    /var/lib/docker/volumes/:
    total 4
    drwx------. 3 0 0   77 Mar 15 10:50 .
    drwx-----x. 9 0 0 4096 Nov 18 22:04 ..
    drwxr-xr-x. 3 0 0   18 Mar 15 10:50 7f9d945c3b3352308a44878a5da9e6046d63e34fafbac36486f4b94f5d372b61

    /var/lib/docker/volumes/7f9d945c3b3352308a44878a5da9e6046d63e34fafbac36486f4b94f5d372b61:
    total 0
    drwxr-xr-x. 3 0 0 18 Mar 15 10:50 .
    drwx------. 3 0 0 77 Mar 15 10:50 ..
    drwxr-xr-x. 2 0 0  6 Mar 15 10:50 _data

    /var/lib/docker/volumes/7f9d945c3b3352308a44878a5da9e6046d63e34fafbac36486f4b94f5d372b61/_data:
    total 0
    drwxr-xr-x. 2 0 0  6 Mar 15 10:50 .
    drwxr-xr-x. 3 0 0 18 Mar 15 10:50 ..


Examples:

    >>> docker_dirs = shared[DockerVolumesDir]
    >>> '/var/lib/docker/volumes' in docker_dirs
    True
    >>> docker_dirs.dirs_of('/var/lib/docker/volumes')
    ['.', '..', '97d7cd1a5d8fd7730e83bb61ecbc993742438e966ac5c11910776b5d53f4ae07']
    >>> '/var/lib/docker/volumes/97d7cd1a5d8fd7730e83bb61ecbc993742438e966ac5c11910776b5d53f4ae07' in docker_dirs
    True
    >>> docker_dirs.dirs_of('/var/lib/docker/volumes/97d7cd1a5d8fd7730e83bb61ecbc993742438e966ac5c11910776b5d53f4ae07')
    ['.', '..', '_data']