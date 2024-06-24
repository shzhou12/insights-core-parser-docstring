LVDisplay - command ``/sbin/lvdisplay``
=======================================

The normal lvdisplay content looks like this::

  Adding lvsapp01ap01:0 as an user of lvsapp01ap01_mlog
  --- Volume group ---
  VG Name               vgp01app
  ...
  VG Size               399.98 GiB
  VG UUID               JVgCxE-UY84-C0Gk-8Cmn-UGXu-UHo0-9Qa4Re
  --- Logical volume ---
  global/lvdisplay_shows_full_device_path not found in config: defaulting to 0
  LV Path                /dev/vgp01app/lvsapp01ap01-old
  LV Name                lvsapp01ap01-old
  ...
  VG Name                vgp01app
  --- Logical volume ---
  global/lvdisplay_shows_full_device_path not found in config: defaulting to 0
  LV Path                /dev/vgp01app/lvsapp01ap02
  LV Name                lvsapp01ap02
  ...
  VG Name                vgp01app

The data is compiled into two keys in the ``data`` attribute:

* ``Logical volume``: a list of logical volume dictionaries.
* ``Volume group``: a list of volume group dictionaries.

The keys in each dictionary correspond to the headings found in the
output - for example, the keys in each ``Volume group`` list entry will
include ``VG Name``, ``VG Size``, etc.

In addition, the ``debug`` key in both the ``data`` attribute dictionary
and the ``Logical volume`` and ``Volume group`` dictionaries stores any
debug or warning messages found while parsing the output for that section.

Logical volumes are also available as a dictionary in the ``lvs`` property
and volume groups in the ``vgs`` property, both arranged by name.  Both
contain the same information as the associated list entry in the ``volumes``
dictionary.

Examples:

    >>> lvs = shared(LvDisplay)
    >>> 'volumes' in lvs # direct access via LegacyItemAccess
    True
    >>> 'debug' in lvs.data['volumes'] # access via data property
    True
    >>> for lv in lvs.data['volumes']['Logical volume']:
    ---     print lv['LV Name']
    ---
    lvsapp01ap01-old
    lvsapp01ap02
    >>> lvs.lvs['lvsapp01ap02']['VG Name'] # access to LVs by name
    'vgp01app'
    >>> lvs.vgs['vgp01app']['VG Size'] # access to VGs by name
    '399.98 GiB'