ClusterConf - file ``/etc/cluster/cluster.conf``
================================================

Stores a filtered set of lines from the cluster config file.  Because of the
filtering, the content as a whole will not parse as XML.  We use a
:class:`insights.core.LogFileOutput` parser class because, sadly, it's
easiest.