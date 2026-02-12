---
layout: default
title: Helm Linting
parent: DevOps
last_modified_date: 12.02.2026 10:00
---

Lint charts locally without installing Helm:

```bash
# Using chart-testing
docker run --rm -v ${PWD}:/repo -w /repo \
  quay.io/helmpack/chart-testing \
  ct lint --charts chart --validate-maintainers=false

# Alternative with helm3-ci
docker run --rm -v ${PWD}:/repo -w /repo \
  ventx/helm3-ci:latest \
  ct lint --charts chart --validate-maintainers=false
```

**Note:** Replace `${PWD}` with `$(pwd)` on Linux/Mac or use absolute path on Windows.
