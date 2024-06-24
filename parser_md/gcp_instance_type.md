GCPInstanceType
===============

This parser simply reads the output of command
``curl http://metadata.google.internal/computeMetadata/v1/instance/machine-type -H 'Metadata-Flavor: Google'``,
which is used to check the machine type of the Google instance of the host.

For more details, See:
- https://cloud.google.com/compute/docs/machine-types
- https://cloud.google.com/compute/docs/storing-retrieving-metadata#api_4