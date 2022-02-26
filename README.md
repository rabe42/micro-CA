# micro-CA
A skeleton repository to setup a private certfication authority (CA) with openssl.

## Overview
This repository provides a collection of simple purly open-ssl related commands to setup a small private certification authority as the root of a private public key infrastructure. It is not intended to be used in a productive environment, as it provides no protection of the private key of the CA. 

It can be considered as a good starting point in learning about the role of a CA in an PKI. A know-how which is important, in establishing a zero trust environment also in small businesses or even in the private environment.

It is *not* the intention of this module to teach public/private keys and their concepts. There are enough ressources outside available which **should** be read before creating and using a CA.

## Basic Concepts
The root directory contains the configuration file for the CA in the `CA.conf` file. In addition the a number of shell scripts are provided:

Script Name         | Description
--------------------|---------------------------------------
`init`              | Creates all files neccessary for a CA
`examine-csr`       | Output the content of the CSR to stdout for examination.
`examine-crt`       | Output the content of a CRT to stdout for examination.
`create-server-crt`   | Creates a certificate and private key which might be used by a service. (DNS required)
`create-client-crt`   | Creates a certificate and private key which might be used by a client and or user.
`validate`          | Checks, if the certficate is valid and issued by this CA.
`revoke-crt`        | Revokes the certificate by adding it to the CRL.

These scripts allow to do the basic operations of a CA. In addition a script to create private keys and certificate requests are provided.

Script Name      | Description
-----------------|---------------------------------------
`rsa-client-csr` | Creates a private rsa key (4096 bit)  and an certifcate signature request (CSR) for the public key.
`rsa-server-csr` | Creates a private rsa key (4096 bit) for a server and a certificate request for the public key.

## CA Commands
### init
The init command will initialize the needed files and directories. It also creates the first CA private key and self signed root certificate in the new created directory CA.

In the same time it creates also an empty certificate revocation list, which should be used during the 

### create-server-crt
Creates a certificate where minitmum one DNS entry is required. This command takes a certificate request file in PEM format, as a parameter, checks if the domain name and a E-Mail address is provided. The result is a PEM file with the certificate, signed by this CA.

### create-client-crt
Creates a certificate of a client or user. A unique Id for the client should be provided, which allows the identification of the requestor.

### validate
Checks if the certificate is valid and signed by the CA. Beside the signiture it checks if the provided certificate is not on the CRL and is still in the time period, defined at creation time of the certificate.

## RSA Commands
These commands are not really part of the CA, but comes in handy to demonstrate how the clients or users may be provided with an simple way to create there private keys and certificate requests. 

To really leverage on the PKI, it is important, that the users are able to do this step by their own.

### rsa-client-csr
Creates a private key and derives a certificate signing request (CSR) from it. This may be signed with the CA signing command.

### rsa-server-csr
Creates a private key for a server and derives a signing request (CSR) from it. In contrast to the client certificate, a domain name (FQDN) must be provided in this case. In a TLS context, the client can check, if the domain name of the certificate matches the name of the domain.

## Use Cases
### Create a new CA