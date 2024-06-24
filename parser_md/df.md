Disk free space commands
========================

Module for the processing of output from the ``df`` command.  The base class
``DiskFree`` provides all of the functionality for all classes.
Data is avaliable as rows of the output contained in one ``Record`` object
for each line of output.

Parsers contained in this module are:

DiskFree_LI - command ``df -li``
--------------------------------

DiskFree_ALP - command ``df -alP``
----------------------------------

DiskFree_AL - command ``df -al``
--------------------------------