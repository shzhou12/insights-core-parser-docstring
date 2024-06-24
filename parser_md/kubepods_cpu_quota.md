KubepodsCpuQuota - CPU quota for each Kubernetes pod
====================================================

This parser reads the content of ``/sys/fs/cgroup/cpu/kubepods.slice/kubepods-burstable.slice/*.slice/cpu.cfs_quota_us``.