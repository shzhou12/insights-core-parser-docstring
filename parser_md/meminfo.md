meminfo - file ``/proc/meminfo``
================================

This suite of parsers deals with various parts of the contents of
``/proc/meminfo``.  They store the data for many different groupings of
memory usage information as key-value pairs and attributes.  Key strings are
converted to lower case, and all values are stored as integers.  Data stored
in kilobytes (i.e. everything but the hugepage values) are converted to bytes
by multiplying by 1024.

All keys are stored in the parser class as properties.  The information
relevant to particular uses of memory are also available in the following
properties:

``swap``: for swap related information:

* ``total`` - the *SwapTotal* information
* ``free`` - the *SwapFree* information
* ``cached`` - the *SwapCached* information
* ``used`` - total - (free + cached)

``anon``: for anonymous page information:

* ``active`` - the *Active(anon)* information
* ``inactive`` - the *Inactive(anon)* information
* ``pages`` - the *AnonPages* information

``file``: for file mapping information:

* ``active`` - the *Active(file)* information
* ``inactive`` - the *Inactive(file)* information

``slab``: for SLAB allocator information:

* ``total`` - the *Slab* information
* ``reclaimable`` - the *SReclaimable* information
* ``unreclaimable`` - the *SUnreclaim* information

``huge_pages``: for HugePage allocator information:

* ``total`` - the *Hugepages_Total* information
* ``free`` - the *Hugepages_Free* information
* ``reserved`` - the *Hugepages_Rsvd* information
* ``surplus`` - the *Hugepages_Surp* information
* ``size`` - the *HugepageSize* information
* ``anon`` - the *AnonHugepages* information

``huge_pages`` also contains two properties to help parsers determine whether
huge pages are in use:

* ``using`` - are huge pages in use?  Is *Hugepages_Total* > 0?
* ``using_transparent`` - are transparent huge pages in use?  Is
  *AnonHugePages* > 0?


``commit``: for memory overcommit information:

* ``total`` - the *Committed_As* information
* ``limit`` - the *CommitLimit* information

``vmalloc``: for virtual memory allocation information:

* ``total`` - the *VMAllocTotal* information
* ``used`` - the *VMAllocUsed* information
* ``chunk`` - the *VMAllocChunk* information

``cma``: the CMA information:

* ``total`` - the *CMAllocTotal* information
* ``free`` - the *CMAllocFree* information

``direct_map``: the direct memory map information

* ``kb`` - the *DirectMap4K* information
* ``mb`` - the *DirectMap2M* information
* ``gb`` - the *DirectMap1G* information

Sample data::

    MemTotal:        8009912 kB
    MemFree:          538760 kB
    MemAvailable:    6820236 kB
    Buffers:          157048 kB
    Cached:          4893932 kB
    SwapCached:          120 kB
    Active:          2841500 kB
    Inactive:        2565560 kB
    Active(anon):     311596 kB
    Inactive(anon):   505800 kB
    Active(file):    2529904 kB
    Inactive(file):  2059760 kB
    ...

Examples:

    >>> mem = shared[MemInfo]
    >>> m.data.['memtotal'] # Old style accessor
    8202149888
    >>> mem.total # New property-based accessor
    8202149888
    >>> mem.used # Calculated
    7650459648
    >>> m.swap.total
    3221221376
    >>> m.swap.free
    3211624448
    >>> m.swap.used # Calculated
    9474048