AWSInstanceID
=============

These parsers read the output of commands to collect identify information
from AWS instances.

AWSInstanceIdDoc - ``curl -s http://169.254.169.254/latest/dynamic/instance-identity/document``
-----------------------------------------------------------------------------------------------

AWSInstanceIdPkcs7 - ``curl -s http://169.254.169.254/latest/dynamic/instance-identity/pkcs7``
----------------------------------------------------------------------------------------------

AWSPublicIpv4Addresses - ``curl -s http://169.254.169.254/latest/meta-data/public-ipv4``
----------------------------------------------------------------------------------------

AWSPublicHostname ``curl -s http://169.254.169.254/latest/meta-data/public-hostname``
-------------------------------------------------------------------------------------