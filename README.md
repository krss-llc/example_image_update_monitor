# Container Image Update Monitor

## Overview
Automated GitHub Action that tracks upstream container base image digests and creates alerts when updates are detected.

## The Problem
Container supply chain security requires tracking base image updates, but manual digest checking is unreliable and creates security blind spots.

## The Solution
An event-driven workflow that:
- Monitors Microsoft Container Registry base image digests
- Triggers only on identity (SHA256) changes
- Opens GitHub Issues for maintainer review
- Persists digest history in Git

## Architecture
```
.
├── .github/workflows/check-base-image.yml  # Main workflow
├── digest.txt                            # Current image digest
└── README.md                             # This file
```

## Usage
```yaml
# In your workflow dispatch:
workflow_dispatch:
  inputs:
    force_update:
      description: 'Force digest check'
      required: false
```

## Security Model
- **Immutable Tracking:** SHA256 digests ensure image integrity
- **Human-in-the-loop:** Issues created for manual review before rebuild
- **No auto-deploy:** Changes never automatically applied

## Configuration
Set these repository secrets:
- `IMAGE_NAME` - Full image path (e.g., `mcr.microsoft.com/devcontainers/base`)
- `CRON_SCHEDULE` - When to check (default: `0 8 * * 1-5` - weekdays 8AM EST)

## License
MIT