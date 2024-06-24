FcoeadmI - command ``fcoeadm -i``
=================================

Module for parsing the output of command ``fcoeadm -i``. The bulk of the
content is split on the colon and keys are kept as is. Lines beginning
with 'Description', 'Revision', 'Manufacturer', 'Serial Number', 'Driver'
,'Number of Ports' are kept in a dictionary keyed under each of these names.
Lines beginning with 'Symbolic Name', 'OS Device Name', 'Node Name', 'Port Name',
'FabricName', 'Speed', 'Supported Speed', 'MaxFrameSize', 'FC-ID (Port ID)',
'State' are kept in a sub-dictionary keyed under each these names. All the
sub-dictionaries are kept in a list keyed in 'Interfaces'.