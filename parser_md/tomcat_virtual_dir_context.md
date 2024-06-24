Parsers for usage of VirtualDirContext option in Tomcat config files
====================================================================

This module provides the following parsers:

TomcatVirtualDirContextFallback
-------------------------------

This is a parser for a command for finding config files in default location:

``/usr/bin/find /usr/share -maxdepth 1 -name 'tomcat*' -exec grep -R -s 'VirtualDirContext' --include '*.xml' '{}' +``

It is especially useful if the Tomcat server is not running.


TomcatVirtualDirContextTargeted
-------------------------------

This is a parser for a command for finding config files in the custom location defined in a command
line:

``/bin/grep -R -s 'VirtualDirContext' --include '*.xml' {catalina}``

Where ``catalina`` variable is computed as following:

``/bin/ps auxww | awk '/java/ { match($0, "\-Dcatalina\.home=([^[:space:]]+)", a); match($0, "\-Dcatalina\.base=([^[:space:]]+)", b); if (a[1] != "" || b[1] != "") print a[1] " " b[1] }'``


Both parsers detect whether there are any config files which contain VirtualDirContext.

Sample input::

    /usr/share/tomcat/conf/server.xml:    <Resources className="org.apache.naming.resources.VirtualDirContext"

Examples::

    >>> shared[TomcatVirtualDirContextFallback].data
    {'/usr/share/tomcat/conf/server.xml':
     ['    <Resources className="org.apache.naming.resources.VirtualDirContext"'],
     }