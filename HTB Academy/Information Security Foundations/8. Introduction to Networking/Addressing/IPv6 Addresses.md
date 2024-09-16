IPv6 Overview

IPv6 is the successor to IPv4 and offers several improvements over its predecessor. Here are some key points:
    Bit Length: IPv6 addresses are 128 bits long, compared to IPv4's 32-bit addresses.
    Addressing Range: IPv6 provides a vast address space (~340 undecillion) versus IPv4’s ~4.3 billion addresses.
    Representation: IPv4 addresses are represented in decimal format, while IPv6 addresses use hexadecimal notation.
    Dynamic Addressing: IPv4 uses DHCP, while IPv6 uses SLAAC (Stateless Address Autoconfiguration) and DHCPv6.
    IPsec: IPv6 mandates IPsec for encryption, whereas it's optional in IPv4.

IPv6 Features:
    Larger Address Space: IPv6 offers a significantly larger address space than IPv4.
    Address Self-Configuration (SLAAC): Allows devices to configure their own IP addresses without a DHCP server.
    Multiple Addresses per Interface: A single interface can have multiple IPv6 addresses.
    Faster Routing: Improved routing efficiency compared to IPv4.
    End-to-End Encryption: IPsec is mandatory, enhancing security.
    Large Data Packages: Supports data packets up to 4 GB.

IPv6 Address Types:
    Unicast: Addresses for a single interface.
    Anycast: Addresses for multiple interfaces; only one receives the packet.
    Multicast: Addresses for multiple interfaces; all receive the same packet.
    Broadcast: Does not exist in IPv6; realized using multicast addresses.

Hexadecimal System:
    Hexadecimal Notation: Used to simplify the representation of binary data.
        Decimal: 0-9
        Hex: 0-F (where A=10, B=11, C=12, D=13, E=14, F=15)
    Conversion Example:
        IPv4 Address (192.168.12.160):
            Binary: 11000000.10101000.00001100.10100000
            Hexadecimal: C0.A8.0C.A0

IPv6 Address Representation:
    Format: Consists of 16 bytes, represented in hexadecimal notation.
        Full IPv6 Address: fe80:0000:0000:0000:dd80:b1a9:6687:2d3b/64
        Short IPv6 Address: fe80::dd80:b1a9:6687:2d3b/64
    Notation Rules (RFC 5952):
        All alphabetical characters are written in lowercase.
        Leading zeros in each block are omitted.
        One or more consecutive blocks of 4 zeros can be shortened by two colons (::).
        The shorthand (::) can be used only once in an address.

IPv6 Address Components:
    Network Prefix: Identifies the network, subnet, or address range.
    Interface Identifier: Also known as Suffix, typically derived from the MAC address of the interface. The default prefix length is /64, but other common prefixes are /32, /48, and /56.

Dual Stack:
    IPv4 and IPv6 can coexist, allowing for a gradual transition from IPv4 to IPv6.

Address Assignment:
    The Internet Assigned Numbers Authority (IANA) is responsible for assigning both IPv4 and IPv6 addresses and their associated network portions.