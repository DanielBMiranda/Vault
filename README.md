# Vault

The Vault is a system developed in Python for securely storing and retrieving encrypted files, accessible only to authorized users or groups. The project involved building both a client application that communicates with the server over a secure channel, and a multithreaded server capable of managing multiple requests simultaneously.

# Usage Guide

## Setup and Running the Program

To use this program, start by running the server with the following command:

```bash
python3 vault-d.py
```

## Deposit a document accessible by a single user

Run the client with the specified public key and file path to deposit a document:

```bash
python3 vault-c.py -d publicKey -f filePath
```

To generate the necessary RSA key files, use the following commands:

```bash
# Generate a 2048-bit RSA private key
openssl genrsa -out [Private Key] 2048

# Generate a public key from the private key
openssl rsa -in [Private Key] -pubout -out [Public Key]
```

Decrypt an encrypted key received from the server:
```bash
openssl rsautl -decrypt -in [Encrypted Key] -oaep -out [Output] -inkey [Private Key]
```

Access a stored document with the specified hash and decrypted key:
```bash
python3 vault-c.py -w decryptKey -h fileHash -f filePath
```

## Deposit a document accessible by multiple users

This type of deposit utilizes Shamir's Secret Sharing and, as such, requires a minimum of `n` out of `m` total participants for successful decryption.

```bash
python3 vault-c.py -f filePath -s n m -d pubKey1 pubKey2 ...
```

Access the document as part of a group with an index for tracking requests
```bash
python3 vault-c.py -w decryptKey -i index -h fileHash -f filePath
```

Create RSA keys using the createKeys.sh script, specifying key counts
```bash
bash createKeys.sh 1 5
```

Decrypt an encrypted key from the server using decryptKey.sh script
```bash
bash decryptKey.sh [Encrypted Key] [Output] [Private Key]
```

# Contributors:

[Rui Carvalho](https://github.com/RuiC10)
[Ana Luísa](https://github.com/Analucar)