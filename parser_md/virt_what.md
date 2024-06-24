VirtWhat - Command ``virt-what``
================================

Parses the output of the ``virt-what`` command to check if the host is running
in a virtual machine.

Sample input::
    kvm

Examples:
    >>> vw = shared[VirtWhat]
    >>> vw.is_virtual
    True
    >>> vw.is_physical
    False
    >>> vw.generic
    'kvm'
    >>> 'aws' in vw
    False

Note:
    For ``virt-what-1.13-8`` or older on RHEL7, the command fails when running
    without an environment (or very restricted environment), and reports below
    error::

        virt-what: virt-what-cpuid-helper program not found in $PATH