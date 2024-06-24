QemuConf - file ``/etc/libvirt/qemu.conf``
==========================================

The ``/etc/libvirt/qemu.conf`` file is in a key-value format, but there are several lines for one value.

Given a file containing the following test data::

   vnc_listen = "0.0.0.0"
   vnc_auto_unix_socket = 1
   vnc_tls = 1
   vnc_tls_x509_cert_dir = "/etc/pki/libvirt-vnc"
   security_driver = "selinux"
   cgroup_device_acl = [
    "/dev/null", "/dev/full", "/dev/zero",
    "/dev/random", "/dev/urandom",
    "/dev/ptmx", "/dev/kvm", "/dev/kqemu",
    "/dev/rtc","/dev/hpet", "/dev/vfio/vfio"
    ]

Example:
    >>> config = shared[QemuConf]
    >>> config.get('vnc_listen')
    '0.0.0.0'
    >>> config.get('vnc_tls')
    '1'
    >>> "/dev/random" in config.get('cgroup_device_acl')
    True