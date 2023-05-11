# How to create ssl certificate for local test environment


Hi there, it's me again! Today, I'll guide you through the process of creating an SSL certificate for your local test environment on Ubuntu 20.04. It's going to be a fun ride, so let's get started!

In bash shell, run these commands:
<!--more-->

## Create Certificate Authority
```bash
openssl genrsa -des3 -out rootCA.key 2048
```
Input some information as required. Please notice to save **pass phrase for rootCA.key** in a safe place. You will use this many times later.

```bash
openssl req -x509 -new -nodes -key rootCA.key -sha256 -days 3650 -out rootCA.pem
```
Change days as you want. 3650 days mean 10 years. :).

Now we will have two files: **rootCA.key** and **rootCA.pem**. Now you ara a certificate provider.

In your client PC, open browser (chrome, firefox...) and import file **rootCA.pem** to tell browser "I am a valid certificate provider" :).

<!--more-->

## Generate rsa for domain

### Create private key

```bash
openssl genrsa -out YOUR_DOMAIN_NAME.key 2048
```

### Create csr

```bash
openssl req -new -key YOUR_DOMAIN_NAME.key -out YOUR_DOMAIN_NAME.csr
```

### Create file SAN file
```bash
vi YOUR_DOMAIN_NAME.ext
```
Content:
```bash
authorityKeyIdentifier=keyid,issuer
basicConstraints=CA:FALSE
keyUsage = digitalSignature, nonRepudiation, keyEncipherment, dataEncipherment
subjectAltName = @alt_names

[alt_names]
DNS.1 = <YOUR DOMAIN 2 HERE>
DNS.2 = <YOUR DOMAIN 2 HERE>
```
Please notice that you can add as **much DNS.x** as you want.

## Create domain certificate
```bash
openssl x509 -req -in YOUR_DOMAIN_NAME.csr -CA rootCA.pem -CAkey rootCA.key -CAcreateserial -out YOUR_DOMAIN_NAME.crt -days 3650 -sha256 -extfile YOUR_DOMAIN_NAME.ext
```
Change the days as you want. 3650 days mean about 10 years.

Now you have **crt, csr, key** files for domain. Copy these files to web server (example nginx) and config.

