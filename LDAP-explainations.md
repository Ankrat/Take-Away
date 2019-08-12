source: [Wikipedia](https://en.wikipedia.org/wiki/Lightweight_Directory_Access_Protocol)

# LDAP



## Definition

The Lightweight Directory Access Protocol (LDAP) is an open, vendor-neutral,
industry standard application protocol for accessing and maintaining
distributed directory information services
over an Internet Protocol (IP) network.

## Protocol overview

A client starts an LDAP session by connecting to an LDAP server,
called a Directory System Agent (DSA), by default
on TCP and UDP port 389, or on port 636 for LDAPS (LDAP over SSL, see below).

The client then sends an operation request to the server,
and the server sends responses in return.

With some exceptions,
the client does not need to wait for a response before sending the next request,
and the server may send the responses in any order.

All information is transmitted using Basic Encoding Rules (BER).

### Example of Operations

- StartTLS (use the LDAPv3 Transport Layer Security (TLS) extension for a secure connection)
- Bind (authenticate and specify LDAP protocol version)
- Search (retrieve directory entries)
- Compare (test if a named entry contains a given attribute value)
- Add a new entry
- Delete an entry
- Modify an entry
- Modify Distinguished Name (DN) (move or rename an entry)
- Abandon (abort a previous request)
- Extended Operation (generic operation used to define other operations)
- Unbind (close the connection (not the inverse of Bind))

### Example of Entry:

An entry consists of a set of attributes.

An attribute has a name (an attribute type or attribute description) and one or more values. The attributes are defined in a schema (see below).

Each entry has a unique identifier: its Distinguished Name (DN).

- Relative Distinguished Name (RDN), constructed from some attribute(s) in the entry,
- followed by the parent entry's DN.

Think of the DN as the full file path and the RDN as its relative filename in its parent folder (e.g. if /foo/bar/myfile.txt were the DN, then myfile.txt would be the RDN).

An entry can look like this when represented in LDAP Data Interchange Format (LDIF)
(LDAP itself is a binary protocol):

```LDIF
dn: cn=John Doe,dc=example,dc=com
cn: John Doe
givenName: John
sn: Doe
telephoneNumber: +1 888 555 6789
telephoneNumber: +1 888 555 1232
mail: john@example.com
manager: cn=Barbara Doe,dc=example,dc=com
objectClass: inetOrgPerson
objectClass: organizationalPerson
objectClass: person
objectClass: top
```

- **dn** is the distinguished name of the entry; it is neither an attribute nor a part of the entry.

- **cn=John Doe** is the entry's RDN (Relative Distinguished Name),

- **dc=example,dc=com** is the DN of the parent entry, where "dc" denotes 'Domain Component'.

- The other lines show the attributes in the entry.

Attribute names are typically mnemonic strings, like "cn" for common name, "dc" for domain component, "mail" for e-mail address, and "sn" for surname...
