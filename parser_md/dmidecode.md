DMIDecode - Command ``dmidecode``
=================================

Parses the output of the ``dmidecode`` command to catalogue the hardware
associated with the system.

In general, DMIdecode recognizes the sections of device information,
separated by blank lines, processed in the following way.

* It uses the descriptor line that precedes the indented device information
  (e.g. 'BIOS Information') as the name for that section, converting the name
  into lower case and replacing spaces with underscores (e.g.
  'bios_information') to look more Pythonic.

* Within each section, data is split up on colons.

* Lines such as 'Characteristics' that end with a colon and have one or more
  further indented lines after them are converted into a list of the values so
  indented.

The common information retrieved from dmidecode is available in several
convenience properties:

* **system_info** - Information about the machine itself
* **bios** - the BIOS information
* **bios_vendor** - the BIOS's 'Vendor' attribute
* **bios_date** - the BIOS's 'Release Date' attribute
* **processor_manufacturer** - the processor's 'Manufacturer' attribute
* **is_present** - this indicates whether dmidecode information was found.

Sample input::

    # dmidecode 2.2
    SMBIOS 2.4 present.
    104 structures occupying 3162 bytes.
    Table at 0x000EE000.
    Handle 0x0000
        DMI type 0, 24 bytes.
        BIOS Information
            Vendor: HP
            Version: A08
            Release Date: 09/27/2008
            Address: 0xF0000
            Runtime Size: 64 kB
            ROM Size: 4096 kB
            Characteristics:
                PCI is supported
                PNP is supported
                BIOS is upgradeable
                BIOS shadowing is allowed
                ESCD support is available
                Boot from CD is supported
                Selectable boot is supported
                EDD is supported
                5.25"/360 KB floppy services are supported (int 13h)
                5.25"/1.2 MB floppy services are supported (int 13h)
                3.5"/720 KB floppy services are supported (int 13h)
                Print screen service is supported (int 5h)
                8042 keyboard services are supported (int 9h)
                Serial services are supported (int 14h)
                Printer services are supported (int 17h)
                CGA/mono video services are supported (int 10h)
                ACPI is supported
                USB legacy is supported
                BIOS boot specification is supported
                Function key-initiated network boot is supported``
    Handle 0x0100
        DMI type 1, 27 bytes.
        System Information
            Manufacturer: HP
            Product Name: ProLiant BL685c G1
            Version: Not Specified
            Serial Number: 3H6CMK2537
            UUID: 58585858-5858-3348-3643-4D4B32353337
            Wake-up Type: Power Switch

Examples:

    >>> dmi = shared[DMIDecode]
    >>> dmi.is_present
    True
    >>> len(dmi['bios_information'])
    1
    >>> dmi['bios_information'][0]['vendor']
    'HP'
    >>> dmi.bios_vendor
    'HP'
    >>> dmi.bios_date
    datetime.date(2008, 9, 27)
    >>> len(dmi.bios['characteristics'])
    20
    >>> dmi.bios['characteristics'][0]
    'PCI is supported'
    >>> dmi.system_uuid == '58585858-5858-3348-3643-4D4B32353337'
    True