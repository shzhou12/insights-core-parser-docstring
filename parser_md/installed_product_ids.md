Installed product IDs
=====================

InstalledProductIDs - command ``find /etc/pki/product-default/ /etc/pki/product/ -name '*pem' -exec rct cat-cert --no-content '{}' \;``
---------------------------------------------------------------------------------------------------------------------------------------

This module provides a parser for information about certificates for
Red Hat product subscriptions.