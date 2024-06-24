DockerList - command ``/usr/bin/docker (images|ps)``
====================================================

Parse the output of command "docker_list_images" and "docker_list_containers",
which have very similar formats.

The header line is parsed and used as the names for the remaining columns.
All fields in both header and data are assumed to be separated by at least
three spaces.  This allows single spaces in values and headers, so headers
such as 'IMAGE ID' are captured as is.

If the header line and at least one data line are not found, no data is
stored.

Each row is stored as a dictionary, keyed on the header fields.  The data is
available in two formats:

* The old format is a list of row dictionaries.
* The new format stores each dictionary in a dictionary keyed on the value of
  a given field, given by the subclass.