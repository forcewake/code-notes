---
title: OpenSSL
category: Unix
order: 4
---

## Getting Self Signed SSL Certificates (.pem and .pfx)

### Online Service

[Cert-Depot](http://www.cert-depot.com./) - It can create certificates in both unencrypted PEM format, and PFX.

### Terminal

Install openssl package for your operating system Generating a private key:

```bash
openssl genrsa 2048 > some-private.pem
```

Generating the self signed certificate:

```bash
openssl req -x509 -new -key some-private.pem -out some-public.pem
```

If required, creating PFX:

```bash
openssl pkcs12 -export -in some-public.pem -inkey some-private.pem -out some-cert.pfx
```