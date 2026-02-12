---
layout: default
title: OpenSSL Certificate Generation
parent: DevOps
last_modified_date: 10:00 12.02.2026
---

## Testing Stack with Secrets

```yaml
version: '3.9'
services:
  app:
    image: nginx
    secrets:
      - app-secret

secrets:
  app-secret:
    external: true
```

## Adding Certificate Secrets

### 1. Encode certificate

```bash
# Linux/Mac
base64 -w0 certificate.pfx

# Windows PowerShell
[Convert]::ToBase64String([IO.File]::ReadAllBytes("certificate.pfx"))
```

### 2. Create secret in Portainer

- Navigate to Secrets
- Click "Add secret"
- **Encode secret: OFF** (already base64 encoded)
- Paste encoded value
- Save

### 3. Reference in stack

```yaml
services:
  app:
    secrets:
      - source: cert-secret
        target: /app/cert.pfx

secrets:
  cert-secret:
    external: true
```
