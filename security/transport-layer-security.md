### <center> TLS - Transport Layer Security

* Provides over-the-wire protection mechanisms
    * Authentication
    * Message integrity
    * Data encryption
* An evolution from Secure Sockets Layer (SSL)
    * TLSv1 initiated after SSLv3
    * SSL is often used when TLS is meant
        * SSL has many well-known vulnerabilities (including POODLE)
    * TLS 1.2 is available; TLS 1.3 is a draft RFC

---

### <center> TLS Authentication

* TLS uses certificates to authenticate a remote party
* Certificates rely on asymmetric encryption, usually RSA
* A certificate includes the owner's public key and identifying information
    * The certificate issuer (authority)
    * Date to which the certificate is deemed valid
    * Other attributes as required
* A certificate is signed by its issuer
    * Can be self-signed
    * Can be a well-known Certificate Authority (CA)

---

### <center> Certificate Authority (CA)

* A trusted third party between a client and service
    * Maintains its own certificate
    * Used as guarantor to issue and sign other certificates
* Well-known public CAs such as VeriSign reply on reputation
    * And charge for the service they provide
* In-house certificate servers are common in large enterprises
    * MS Active Directory includes Certificate Services
    * A certificate issued by one CA to another is an intermediate certificate
* A root CA relies on a self-signed certificate
    * This a reputation for safekeeping is a key asset

---

### <center> How Clients Establish Trust with Services

* Client wants to negotiate a connection with a Service over TLS
* The Service has a certificate issued by CA1
* Client must trust CA1 for this to work
    * Client has or adds CA1's certificate to its trust store
* If the Service must be able to trust the Client too, same process
    * Client trusts Service => one-way SSL (that is, TLS)
    * Service also trusts Client => two-way SSL
* The Client only needs a certificate if the Service must trust it

---

### <center> Certificate Chaining

* CA1 has issued a certificate to (intermediary) CA2
* Service gets its certificate from CA2
* CA1 cannot verify the Service certificate
    * Client must trust/use CA2 directly
    * Or use a chain provided by CA2 that leads to its root (CA1)
* This Service's chain would be simple: CA2 -> CA1
    * If Client trusts CA1, Service can just present CA2's chain
    * Important because Client trust stores tend to contain root CA's only
    * If more intermediates are involved, they must be included in the chain

---

### <center> Certificate Formatting

* You can encode a certificate multiple ways
    * DER ([Distinguished Encoding Rules](http://www.planetlarg.net/encyclopedia/ssl-secure-sockets-layer/der-distinguished-encoding-rules-certificate-encoding)): binary encoding
    * Privacy Enhanced Email (PEM): textual representation (Base64) of DER
        * Exchange-friendly format 
* Java services in EDH use a Java Keystore; all others use PEM
    * The `openssl` library has utilities to manage/convert formats
    * Java `keytool` utility works with Keystore objects

---

### <center> Certificate Requests

* To obtain a certificate from a CAl
    * Generate a certificate signing request (CSR)
    * Requires a private key (RSA) and identifying information
* A CSR is Base64-encoded (for email transfer) and contains
    * The public key associated with your private key
    * The identifying information you provide
* Or you can self-sign your CSR
* The result includes the public key and authorization attributes
    * `Client Auth` and `Server Auth` are expected attributes
* Some CAs will offer templates for typical authorization requests

---

### <center> What about Encryption or Integrity Checking?

* EDH uses TLS for authentication only
    * Asymmetric encryption is cumbersome for data transfer
    * Very slow, less secure than alternatives
* TLS is used to encrypt symmetric keys that encrypt data
    * AES is the most common symmetric key encryption suite
    * The symmetric key is negotiated between Client and Server
    * The digest for integrity checks is also negotiated (e.g., SHA-256)

---

### <center> Tools to Remember

* Use `openssl s_client ...` to test connections
    * Is the server endpoint using TLS?
    * Is there a certificate chain provided?
    * Would I accept the server's certificate?
    * Can I import the certificates into my trust store?
* Java `keytool`
    * I need to add/remove/modify my keystore
    * I need to verify the password protecting my keystore

---

### <center> Performance Cost

* TLS uses encryption, encryption is expensive
* The `openssl` libraries use AES-NI natively
    * EDH uses the `openssl-devel` package to access it (kinda)
    * TLS uses AES for encryption
* Use the command `hadoop checknative` to check which `openssl` libraries you have
* Stronger encryption requires greater system entropy
    * On bare metal, might be sufficient
    * Install `rng-tools` if the CPU supports Intel RDRAND
    * Otherwise install `haveged` from the EPEL repo 

---

### <center> Putting It All To Use

* Cloudera Manager offers three progressive levels of TLS integration
    * Level 1: wire encrpytion between agents and server
    * Level 2: agents validate the server (one-way trust)
    * Level 3: server validates agents (two-way trust)
* Best to enable TLS before Kerberos
    * So keytabs are protected in-flight
* EDH components that leverage TLS
    * Navigator & HUE web UIs
    * Hive & Impala (secure JDBC/ODBC access)
    * Oozie
    * Hadoop web UIs, MapReduce shuffling

---

### <center> Ben's Lab Environment

* Use the domain `CLOUDERA.LOCAL`
* Centrify is installed on clusters and nodes are AD-registered
* All required certificates available in `/opt/cloudera/security`
* Your PEM key password is `cloudera`
* Anything else that needs a password, `Cloudera!` should work
* All private keys for server certificates are PEM-encoded
* Use public documentation to enable TLS levels 1, 2, and 3 for CM
* Remember you can check certificates with `openssl s_client ...`

---

### <center> Should you run out of things to do

* Enable Active Directory LDAPS authentication
    * Cloudera Manager
    * Cloudera Navigator
    * HUE
    * Impala
* Enable spill encryption for Impala
* Enable Sentry and configure roles for Alice and Bob
* Enable HDFS RPC Encryption and DataNode transfer encryption

