# Experiment 4 – Self-Signed X.509 Digital Certificate Using OpenSSL

## Aim

To generate, inspect, and verify a self-signed X.509 digital certificate using OpenSSL.

## Requirements

* EndeavourOS / Linux
* OpenSSL

## Procedure

### Step 1: Generate RSA Private Key

A **2048-bit RSA private key** was generated using the following command:

```bash
openssl genrsa -out private.key 2048
```

The generated private key was checked for correctness using:

```bash
openssl rsa -in private.key -check
```

### Step 2: Generate Self-Signed X.509 Certificate

A self-signed X.509 digital certificate was generated using the RSA private key:

```bash
openssl req -x509 -new -key private.key -out certificate.crt -days 365
```

During this process, OpenSSL prompts for certificate information such as:

* Country Name
* State or Province
* Locality
* Organization Name
* Common Name
* Email Address

The resulting certificate is valid for **365 days**.

### Step 3: Inspect the Certificate

The details of the generated X.509 certificate were displayed using:

```bash
openssl x509 -in certificate.crt -text -noout
```

The certificate information includes:

* **Subject**
* **Issuer**
* **Public Key**
* **Validity Period**
* **Serial Number**
* **Subject Alternative Name (SAN)**, if configured
* **Digital Signature**
* **Signature Algorithm**

### Step 4: Verify the Certificate

The self-signed certificate was verified using:

```bash
openssl verify -CAfile certificate.crt certificate.crt
```

Since the certificate is **self-signed**, it must be explicitly provided as a trusted certificate using the `-CAfile` option.

A successful verification produces output similar to:

```text
certificate.crt: OK
```

## Result

A **2048-bit RSA private key** and a **self-signed X.509 digital certificate** were successfully generated, inspected, and verified using OpenSSL.
