GRUB configuration files
========================

This parser reads the configuration of the GRand Unified Bootloader, versions
1 or 2.

This is currently a fairly simple parsing process.  Data read from the file
is put into roughly three categories:

* **configs**: lines read from the file that aren't boot options (i.e.
  excluding lines that go in the *title* and *menuentry* sections).  These
  are split into pairs on the first '=' sign.
* **title**: (GRUB v1 only) lines prefixed by the word 'title'.  All following
  lines up to the next title line are folded together.
* **menuentry**: (GRUB v2 only) lines prefixed by the word 'menuentry'.  All
  following lines up to the line starting with '}' are treated as part of one
  menu entry.

Each of these categories is (currently) stored as a simple list of tuples.

* For the **configs** dict, the key-value pairs based on the line, split
  on the first '=' character.  If nothing is found after the '=' character,
  then the value is `''`.

* For the **title** and **menuentry** list, dict of each boot entry is stored.

  * The items will be key-value pairs, e.g. ``load_video`` will be stored
    as ``{'load_video': ''}`` and ``set root='hd0,msdos1'`` will be stored
    as ``{'set': "root='hd0,msdos1'"}``.

.. note::
    For GRUB version 2, all lines between the ``if`` and ``fi`` will be ignored
    due to we cannot analyze the result of the bash conditions.

Parsers provided by this module are:

Grub1Config - file ``/boot/grub.conf``
--------------------------------------

Grub1EFIConfig - file ``/boot/efi/EFI/redhat/grub.conf``
--------------------------------------------------------

Grub2Config - file ``/boot/grub/grub2.cfg``
-------------------------------------------

Grub2EFIConfig - file ``/boot/efi/EFI/redhat/grub.cfg``
-------------------------------------------------------

BootLoaderEntries - file ``/boot/loader/entries/*.conf``
--------------------------------------------------------