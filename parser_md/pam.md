Pluggable Authentication Module configuration
=============================================

This module provides parsing for PAM configuration files.
``PamConf`` is a parser for ``/etc/pam.conf`` files. Sample input is provided
in the examples.

PamConf - file ``/etc/pam.conf``
--------------------------------

Sample file data::

    #%PAM-1.0
    vsftpd      auth        required    pam_securetty.so
    vsftpd      auth        requisite   pam_unix.so nullok
    vsftpd      auth        sufficient  pam_nologin.so
    vsftpd      account     optional    pam_unix.so
    other       password    include     pam_cracklib.so retry=3 logging=verbose
    other       password    required    pam_unix.so shadow nullok use_authtok
    other       session     required    pam_unix.so


Examples:
    >>> type(pam_conf)
    <class 'insights.parsers.pam.PamConf'>
    >>> len(pam_conf)
    7
    >>> pam_conf[0].service
    'vsftpd'
    >>> pam_conf[0].interface
    'auth'
    >>> pam_conf[0].control_flags
    [ControlFlag(flag='required', value=None)]
    >>> pam_conf[0].module_name
    'pam_securetty.so'
    >>> pam_conf[0].module_args is None
    True
    >>> pam_conf.file_path
    '/etc/pam.conf'

PamDConf - used for specific PAM configuration files
----------------------------------------------------

``PamDConf`` is a base class for the creation of parsers for ``/etc/pam.d``
service specific configuration files.

Sample file from ``/etc/pam.d/sshd``::

    #%PAM-1.0
    auth       required     pam_sepermit.so
    auth       substack     password-auth
    auth       include      postlogin
    # Used with polkit to reauthorize users in remote sessions
    -auth      optional     pam_reauthorize.so prepare
    account    required     pam_nologin.so
    account    include      password-auth
    password   include      password-auth
    # pam_selinux.so close should be the first session rule
    session    required     pam_selinux.so close
    session    required     pam_loginuid.so
    # pam_selinux.so open should only be followed by sessions to be executed in the user context
    session    required     pam_selinux.so open env_params
    session    required     pam_namespace.so
    session    optional     pam_keyinit.so force revoke
    session    include      password-auth
    session    include      postlogin
    # Used with polkit to reauthorize users in remote sessions
    -session   optional     pam_reauthorize.so prepare

Examples:

    >>> type(pamd_conf)
    <class 'insights.parsers.pam.PamDConf'>
    >>> len(pamd_conf)
    15
    >>> pamd_conf[0]._errors == [] # No errors in parsing
    True
    >>> pamd_conf[0].service
    'sshd'
    >>> pamd_conf[0].interface
    'auth'
    >>> pamd_conf[0].control_flags
    [ControlFlag(flag='required', value=None)]
    >>> pamd_conf[0].module_name
    'pam_sepermit.so'
    >>> pamd_conf[0].module_args is None
    True
    >>> pamd_conf.file_path
    '/etc/pam.d/sshd'
    >>> pamd_conf[3].module_name
    'pam_reauthorize.so'
    >>> pamd_conf[3].ignored_if_module_not_found
    True

Normal use of the ``PamDConf`` class is to subclass it for a parser.  In
``insights/specs/default.py``::

    pam_sshd = simple_file("etc/pam.d/sshd")

In the parser module (e.g. ``insights/parsers/pam_sshd.py``)::

    from insights import parser
    from insights.parsers.pam import PamDConf
    from insights.specs import Specs

    @parser(Specs.pam_sshd)
    class PamSSHD(PamDConf):
        pass

References:
    http://www.linux-pam.org/Linux-PAM-html/Linux-PAM_SAG.html