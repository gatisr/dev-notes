---
layout: default
title: Trivy Security Scanning
parent: Security
last_modified_date: 10:00 12.02.2026
---

## Filesystem Scan

### High and critical vulnerabilities

```bash
docker run --rm -v .:/var/ aquasec/trivy:latest \
  fs --exit-code 1 --severity HIGH,CRITICAL /var
```

### All vulnerabilities

```bash
docker run --rm -v .:/var/ aquasec/trivy:latest \
  fs --exit-code 0 --severity UNKNOWN,LOW,MEDIUM /var
```

## Docker Image Scan

### High and critical vulnerabilities

```bash
docker build -t temp-image -f Dockerfile . && \
docker save temp-image -o image.tar && \
docker rmi temp-image && \
docker run --rm -v .:/var/ aquasec/trivy:latest \
  image --exit-code 1 --severity HIGH,CRITICAL --input /var/image.tar
```

### All vulnerabilities

```bash
docker build -t temp-image -f Dockerfile . && \
docker save temp-image -o image.tar && \
docker rmi temp-image && \
docker run --rm -v .:/var/ aquasec/trivy:latest \
  image --exit-code 0 --severity UNKNOWN,LOW,MEDIUM --input /var/image.tar
```

**Note:** `--exit-code 1` fails the command if vulnerabilities found (useful for CI/CD).
