GCPNetworkInterfaces
====================

This parser reads the output of a command
``curl -H "Metadata-Flavor: Google" "http://metadata/computeMetadata/v1/instance/network-interfaces/?recursive=true"``,
which is used to fetch external IP address information.

For more details, See: https://cloud.google.com/compute/docs/metadata/overview