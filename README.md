# micro-CA
A skeleton repository to setup a private certfication authority (CA) with openssl.

## Overview
This repository provides a collection of minimal configuration options to setup a really small private certification authority as the root of your private public key infrastructure. 

## Basic Concepts
The root directory contains the configuration file for the CA in the `CA.conf` file. In addition the following shell scripts are provided:

script name        | description
-------------------|---------------------------------------
init               | Creates all files neccessary for a CA
create-service-crt | Creates a certificate and private key which might be used by a service. (DNS required)
create-client-crt  | Creates a certificate and private key which might be used by a client and or user.
validate           | Checks, if the certficate is valid and issued by this CA.

## Commands
### init
The init command will initialize the needed files and directories. It also creates the first CA private key and self signed root certificate in the new created directory CA.

In the same time it creates also an empty certificate revocation list, which should be used during the 

### create-service-crt
Creates a certificate where minitmum one DNS entry is required.

### create-client-crt
Creates a certificate of a client or user. A unique Id for the client should be provided, which allows the identification of the requestor.

### validate
Checks if the certificate is valid and signed by the CA. Beside the signiture it checks if the provided certificate is not on the CRL and is still in the time period, defined at creation time of the certificate.