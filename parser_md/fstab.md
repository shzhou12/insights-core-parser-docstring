FSTab - file ``/etc/fstab``
===========================

Parse the ``/etc/fstab`` file into a list of lines.  Each line is a dictionary
of fields, named according to their definitions in ``man fstab``:

* ``fs_spec`` - the device to mount
* ``fs_file`` - the mount point
* ``fs_vfstype`` - the type of file system
* ``fs_mntops`` - the mount options as a dictionary
* ``fs_freq`` - the dump frequency
* ``fs_passno`` - check the filesystem on reboot in this pass number
* ``raw_fs_mntops`` - the mount options as a string
* ``raw`` - the RAW line which is useful to front-end

``fs_freq`` and ``fs_passno`` are recorded as integers if found, and zero if
not present.

``fs_mntops`` is wrapped as a as a :class:`insights.parsers.mount.MountOpts`
object.  For instance, the option ``rw`` in ``rw,dmode=0500`` may be accessed as
``mnt_row_info.rw`` with the value ``True``, and the ``dmode`` can be accessed
as ``mnt_row_info.dmode`` with the value ``0500``.

This data, as above, is available in the ``data`` property:

* Wrapped as an :class:`FSTabEntry`, each column can also be accessed as an
  attribute with the same name.

The :class:`FSTabEntry` for each mount point is also available via the
:attr:`FSTab.mounted_on` property; the data is the same as that stored in the
:attr:`FSTab.data` list.