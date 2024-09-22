Here are the notes based on the provided text:

### Active Directory Protocols

1. **Protocols Required by Active Directory:**
   - **LDAP**: Lightweight Directory Access Protocol for directory lookups.
   - **Kerberos**: Microsoft’s version of the Kerberos authentication protocol.
   - **DNS**: Domain Name System for locating domain controllers and enabling communication.
   - **MSRPC**: Microsoft implementation of Remote Procedure Call for interprocess communication.

### Kerberos Authentication
- **Overview**: 
  - Default authentication protocol since Windows 2000.
  - Uses mutual authentication to verify both user and server identities.
  - Stateless, relies on tickets instead of user passwords.
  
- **Process**:
  1. User logs in; password is hashed.
  2. KDC (Kerberos Key Distribution Center) verifies user and issues a Ticket Granting Ticket (TGT).
  3. User presents TGT to request a Ticket Granting Service (TGS) ticket.
  4. User presents TGS to access resources.
  
- **Security**:
  - Credentials are not transmitted over the network.
  - KDC does not record previous transactions; relies on valid TGT for subsequent access.

- **Ports**: 
  - Kerberos uses port **88** (TCP/UDP).

### DNS in Active Directory
- **Function**: 
  - Resolves hostnames to IP addresses and enables communication between clients and domain controllers.
  - Uses Service Records (SRV) to locate services within the network.
  - Supports Dynamic DNS for automatic updates to the DNS database.

- **Ports**: 
  - DNS uses port **53** (UDP by default, falls back to TCP if needed).

### LDAP
- **Overview**: 
  - Open-source protocol for directory services, used for authentication in AD.
  - Latest specification: LDAP Version 3 (RFC 4511).
  
- **Function**: 
  - Manages user account and security information.
  - Active Directory listens for LDAP requests.

- **Ports**:
  - LDAP uses port **389**; LDAPS (LDAP over SSL) uses port **636**.

- **Authentication Types**:
  - **Simple Authentication**: Username/password BIND request.
  - **SASL Authentication**: Uses external authentication services (like Kerberos) for binding.

### MSRPC
- **Overview**: 
  - Microsoft's implementation of RPC, facilitating interprocess communication in Windows.

- **Key Interfaces**:
  - **lsarpc**: Manages local security policy and authentication.
  - **netlogon**: Authenticates users and services in the domain.
  - **samr**: Manages the domain account database (users/groups).
    - Used for reconnaissance and administrative tasks.
  - **drsuapi**: Implements Directory Replication Service for multi-DC replication tasks.
    - Can be exploited to copy the Active Directory database.

### Security Considerations
- Organizations should monitor and manage the use of MSRPC and LDAP to prevent unauthorized access and reconnaissance. 


![[dns_highlevel.png]]

![[Kerb_auth.png]]

![[LDAP_auth.png]]


## Questions
- What networking port does Kerberos use?
	- 88
- What protocol is utilized to translate names into IP addresses? (acronym)
	- DNS
- What protocol does RFC 4511 specify? (acronym)
	- LDAP