---
layout: default
title: Kubernetes Secrets
parent: DevOps
---

## Adding Secrets via UI

1. Select Kubernetes environment
2. Click `+` → `Create from input`

### File mapping approach

```yaml
kind: Secret
apiVersion: v1
metadata:
  name: app-secret-key
  namespace: your-namespace
stringData:
  app-secret-key: "myPlainTextSecret123"
type: Opaque
```

### Environment variable approach

```yaml
kind: Secret
apiVersion: v1
metadata:
  name: app-secret
  namespace: your-namespace
stringData:
  SECRET_KEY: "myPlainTextSecret123"
type: Opaque
```
