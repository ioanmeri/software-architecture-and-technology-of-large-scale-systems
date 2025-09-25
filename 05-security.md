# Section 5: Security

- [Module contents overview](#module-contents-overview)
- [Security objectives](#security-objectives)
- Network Security
  - [Symmetric key encryption](#symmetric-key-encryption)
  - [Public key encryption](#public-key-encryption)

---

## Module contents overview

**System Security**

- Network Security
  - Public Key Cryptography
  - Digital Certificates & Signatures
  - HTTPS
  - Firewalls
- Identity Management
  - Credential Transfer
  - Credential Verification
  - Credential Storage
- Access Management
  - Role Based Access
  - OAuth2
  - JWT Tokens
  - Token Verification
- Common Vulnerabilities
  - SQL Injection
  - CSS Attacks
  - XSRF Attacks

---

## Security objectives

- Restricted / Private Access
  - control the access to the system
- Identity of Client
- Identity of Server
  - clients should make sure they are connected to the right system
- Encrypted Data
  - Man In The Middle protection
- Client Access
  - access services they have been authorized to
- Service Access
  - allow only required actions from one service to another
- Data Access
  - make sure data are accessed be rightful clients / services
  - no client should not be able to access authorization data of another client
- Data Privacy
  - make sure we are not leaking private data at logs / reports / user interface
  - user credentials, user health related data, financial data, sensitive data
- Identity Storage
- Grant Storage
- Single Sign On
- Common Vulnerabilities

![Security objectives](assets/images/42.png)

----

## Symmetric key encryption

**Example**: A component in our system is interacting with an external client / or between private components
- Web application working with a browser
- Browser is connected to application through a public Internet
- Everyone has access to the network between the two machines

**Goal**: Make sure the communication between browser / web application remains secure

Can be done with **Symmetric or Single / Secret Key** cryptography

- Key is a set of characters provided by the person who has created the key
- Can be used along with an encryption algorithm to transform plain text into cipher / encrypted text
- In order to read the encrypted text we have to first de-crypt it
- If we use the same key that were used for encryption to decrypt it ➡️ Symmetric Key
- Achieved Privacy / Confidentiality
  - Securely exchanging data between client and server

Any data the browser send can encrypt it using the symmetric key
- anyone in the public network can read this information but cannot make sense of it
- server holds the same key and uses it to decrypt the information

**Limitations**

- We have to share the secret key with untrusted clients

![Symmetric Key](assets/images/43.png)

---

## Public key encryption

Also called as Asymmetric or Public-Private Key encryption

- we have two different keys for encryption and decryption / public and private key
- these two keys form a pair and they originate from the same information
- any key can be designated for public or private
- once the private key is designated, we don't share it with anyone else
- we share only the public key

**Scenario 1**

- Take plain text and encrypt it with Public key ➡️ encrypted text
- Encrypted text can only be decrypted by corresponding private key
- Only the holder of the private key will be able to decrypt the message
  - Only the intended recipient have access to the data

**Scenario 2**

- Encrypt text using private key
- Can be converted to plain text by using the corresponding public key
- Only the person who is holding the private key can create this message
  - Identity of a sender, and the integrity of data as sent by the sender
- Anyone who has public key can decrypt this message

We have achieved the following security objectives:

- Privacy / Confidentiality
- Authentication
  - Prove One's Identity
- Non-Repudiation
  - Only the sender (private key holder) could have sent this message

---



