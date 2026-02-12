---
layout: default
title: OpenSSL Certificate Generation
parent: Security
last_modified_date: 10:00 12.02.2026
---

Generate self-signed certificate with extended key usage:

```bash
openssl req -x509 -newkey rsa:4096 -sha256 -nodes \
  -keyout private.key \
  -out certificate.crt \
  -subj "/CN=YourCommonName" \
  -addext "extendedKeyUsage=serverAuth,clientAuth" \
  -days 3650
```

**Parameters:**

- `-newkey rsa:4096` - 4096-bit RSA key
- `-sha256` - SHA-256 signature
- `-nodes` - no password on private key
- `-days 3650` - valid for ~10 years
- `serverAuth` - TLS server authentication
- `clientAuth` - TLS client authentication

**Output:**

- `private.key` - Private key (keep secure!)
- `certificate.crt` - Public certificate

**For production:** Use proper CA or Let's Encrypt instead of self-signed certificates.
