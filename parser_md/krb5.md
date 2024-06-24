Krb5Configuration - files ``/etc/krb5.conf`` and ``/etc/krb5.conf.d/*``
=======================================================================

krb5 Configuration are ``/etc/krb5.conf`` and ``/etc/krb5.conf.d/*``,
and the content format is similar to ``INI config``, but they include
values that span multiple lines. Multi-line values start with a '{'
and end with a '}', and we join them together by setting the `is_squ`
variable to True while in a multi-line value.

Example:
    >>> krb5_content = '''
    [realms]
     dns_lookup_realm = false
     ticket_lifetime = 24h
     default_ccache_name = KEYRING:persistent:%{uid}
     EXAMPLE.COM = {
      kdc = kerberos.example.com
      admin_server = kerberos.example.com
     }
     pam = {
      debug = false
      krb4_convert = false
      ticket_lifetime = 36000
     }
     [libdefaults]
      dns_lookup_realm = false
      ticket_lifetime = 24h
      EXAMPLE.COM = {
       kdc = kerberos2.example.com
       admin_server = kerberos2.example.com
     }
    # renew_lifetime = 7d
    # forwardable = true
    # rdns = false
    '''.strip()

    >>> from insights.tests import context_wrap
    >>> shared = {Krb5Configuration: Krb5Configuration(context_wrap(krb5_content))}
    >>> krb5_info = shared[Krb5Configuration]
    >>> krb5_info["libdefaults"]["dnsdsd"]
    "false"
    >>> krb5_info["realms"]["EXAMPLE.COM"]["kdc"]
    "kerberos.example.com"
    >>> krb5_info.sections()
    ["libdefaults","realms"]
    >>> krb5_info.has_section("realms")
    True
    >>> krb5_info.has_option("realms", "nosuchoption")
    False
    >>> krb5_info.options("libdefaults")
    ["dns_lookup_realm","ticket_lifetime","EXAMPLE.COM"]