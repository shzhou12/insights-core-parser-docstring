php_ini - file ``/etc/php.ini``
===============================

This module provides the ``PHPConfig`` class parser, for reading the
options in the ``/etc/php.ini`` file.

Typical content of ``/etc/php.ini`` file is::

    [PHP]
    engine = On
    short_open_tag = Off
    precision = 14
    output_buffering = 4096
    zlib.output_compression = Off
    implicit_flush = Off
    unserialize_callback_func =
    serialize_precision = -1
    disable_functions =
    disable_classes =
    zend.enable_gc = On
    zend.exception_ignore_args = On
    zend.exception_string_param_max_len = 0
    expose_php = On
    max_execution_time = 30
    max_input_time = 60
    memory_limit = 128M
    error_reporting = E_ALL & ~E_DEPRECATED & ~E_STRICT
    default_mimetype = "text/html"

The class has one attribute ``data`` which is a nested ``dict`` representing sections
of the input INI file. Each section is represented as ``dict`` where keys are name
of options and values are values of those options.

Example:
    >>> php_conf["PHP"]["default_mimetype"].value
    'text/html'
    >>> php_config.data['PHP']['default_mimetype']
    'text/html'
    >>> php_conf.data['Session']['session.cache_limiter']
    'nocache'
    >>> php_conf["PHP"]["max_execution_time"].value
     30
    >>> php_conf["PHP"]["engine"].value  # 'On' turns to 'True'
    True
    >>> php_conf["PHP"]["short_opeh_tag"].value  # 'Off' turns to 'False'
    False
    >>> php_c['PHP']['precision'].value
    14
    >>> php_conf.get("PHP").get("memory_limit")  # '128M' is converted into bytes
    134217728