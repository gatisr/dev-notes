---
layout: default
title: OSINT Tools with Docker
parent: Security
last_modified_date: 10:21 13.02.2026
---

## PhoneInfoga - Phone Number Investigation

GitHub: [sundowndev/phoneinfoga](https://github.com/sundowndev/phoneinfoga)

Tool for gathering intelligence on phone numbers, including carrier info, location, and potential OSINT footprints.

### Web UI

```bash
docker run --rm -it -p 8080:8080 \
  sundowndev/phoneinfoga serve -p 8080
```

Access at <http://localhost:8080>

### CLI Scan

```bash
docker run --rm -it sundowndev/phoneinfoga scan -n +1234567890
```

## Sherlock - Username Search Across Platforms

GitHub: [sherlock-project/sherlock](https://github.com/sherlock-project/sherlock)

Searches for a given username across hundreds of social media platforms and websites to check availability and profiles.

```bash
docker run --rm -it theyahya/sherlock username
```

## Maigret - Username Search with Web UI

GitHub: [soxoj/maigret](https://github.com/soxoj/maigret)

Advanced username search tool that collects detailed reports from various sites, with optional web interface for viewing results.

```bash
docker run -p 5000:5000 \
  -v ./reports:/app/reports \
  soxoj/maigret:latest \
  maigret --web 5000
```

Access at <http://localhost:5000>

**Reports saved to:** `./reports/` directory

**Note:** Use these tools responsibly and in compliance with applicable laws and platform terms of service.

## Web Check

GitHub: [lissy93/web-check](https://github.com/lissy93/web-check)

Web Check is a tool for checking the status of websites, including uptime, SSL certificate validity, and other security-related information.

```bash
docker run -p 8888:3000 lissy93/web-check
```

then open <http://localhost:8888>
