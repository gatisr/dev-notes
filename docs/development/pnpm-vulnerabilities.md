---
layout: default
title: pnpm Vulnerabilities
parent: Development
---

## 1. Direct Dependencies (Project Packages)

Update version in `package.json`:

```json
{
  "dependencies": {
    "axios": "^0.21.1"  // vulnerable
    "axios": "^1.6.0"   // fixed
  }
}
```

```bash
pnpm install
```

## 2. Transitive Dependencies (Child Packages)

When a vulnerable package is a dependency of your dependency, use overrides:

### Workflow

1. Add override to package.json

  ```json
  {
    "pnpm": {
      "overrides": {
        "semver": "^7.5.4"  // force fixed version globally
      }
    }
  }
  ```

1. Install and update lock

  ```bash
  pnpm install
  ```

1. Remove override from package.json (to see if parent package upgraded it naturally)

  ```bash
  pnpm install
  ```

1. Check if vulnerability is gone

  ```bash
  pnpm audit
  ```

  If vulnerability returns → restore override and keep it
  
  If clean → you're done

## Checking Vulnerabilities

  ```bash
  pnpm audit                    # see all issues
  pnpm audit --fix              # auto-fix where possible
  pnpm why <package-name>       # see dependency chain
  ```

## Tips

- **Specific overrides**: Use `"parent-package>child-package": "version"` for surgical fixes
- **Version ranges**: Use `>=` if you need minimum version (e.g., `"semver": ">=7.5.4"`)
- **Test after**: Always run tests after updating dependencies
- **Review overrides periodically**: Parent packages may upgrade deps in newer versions
