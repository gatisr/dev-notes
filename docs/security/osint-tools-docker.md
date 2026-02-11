---
layout: default
title: OSINT Tools with Docker
parent: Security
---

## PhoneInfoga - Phone Number Investigation

### Web UI

```bash
docker run --rm -it -p 8080:8080 \
  sundowndev/phoneinfoga serve -p 8080
```

Access at `http://localhost:8080`

### CLI Scan

```bash
docker run --rm -it sundowndev/phoneinfoga scan -n +1234567890
```

## Sherlock - Username Search Across Platforms

```bash
docker run --rm -it theyahya/sherlock username
```

## Maigret - Username Search with Web UI

```bash
docker run -p 5000:5000 \
  -v ./reports:/app/reports \
  soxoj/maigret:latest \
  maigret --web 5000
```

Access at `http://localhost:5000`

**Reports saved to:** `./reports/` directory

**Note:** Use these tools responsibly and in compliance with applicable laws and platform terms of service.
