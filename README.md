# Image Update Monitor

## The Problem
Maintaining secure container environments requires tracking upstream base image updates. Manually checking for digest changes is inefficient and prone to human error, creating gaps in supply chain visibility.

## The Solution
An automated GitHub Actions workflow that tracks a container base image digest, detects updates, and automatically opens a GitHub Issue for maintainer review. See [digest.txt](./digest.txt).

## The How
I prioritized an **Event-Driven Security Model**. Rather than polling daily for image changes, this GitHub action triggers an alert only when the "Identity" (Digest) of the base image shifts, reducing noise while ensuring the maintainer is alerted for a manual security validation.

## Key Features
- [ ] Automated digest tracking (Microsoft Container Registry)
- [ ] Version control persistence (digest history)
- [ ] Proactive notification (GitHub Issue creation)
- [ ] Manual override (force_update workflow dispatch)

## Usage
The workflow runs automatically on a weekday schedule (08:00 EST) or can be triggered manually via the GitHub Actions tab.

## Security
- **Immutable Tracking:** By monitoring the SHA256 digest, we ensure the image hash is audited and persisted in Git history.
- **Human-in-the-loop:** The notification creates an Issue, ensuring a security review occurs before any manual rebuilds are triggered.

## License
MIT
