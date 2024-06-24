GCPLicenseCodes
===============

This parser reads the output of a command
``curl -H "Metadata-Flavor: Google" "http://metadata.google.internal/computeMetadata/v1/instance/licenses/?recursive=True"``,
which is used to check whether the google cloud instance is a licensed marketplace instance.

For more details, See: https://cloud.google.com/compute/docs/reference/rest/v1/images/get#body.Image.FIELDS.license_code