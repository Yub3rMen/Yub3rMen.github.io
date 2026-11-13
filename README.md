# Nextcloud — Self-Hosted Cloud Storage for Real Users

**Ubuntu Server · Docker · Nextcloud · Tailscale · User support · Troubleshooting**

**Project status:** Active home-lab service; documentation in progress. This is a guided, hands-on project, not an independently engineered production cloud platform.

## Overview

I host and maintain a Nextcloud instance on my Ubuntu Server, **Nexus**, to provide file access and mobile photo uploads for approved users. I built the service as a practical way to learn Linux administration, containerized applications, networking, remote connectivity, and ongoing support for people who actually rely on the application.

Unlike a one-time simulation, this project requires continued maintenance: user accounts, device onboarding, connection troubleshooting, application updates, and checking whether file uploads work.

## What I worked on

- **Self-hosting:** Deployed Nextcloud as a Docker application on Ubuntu Server.
- **Remote access:** Configured and used Tailscale as a private access path between approved devices and the server.
- **Account management:** Added users and helped them connect phones and other devices.
- **Photo uploads:** Configured Nextcloud mobile uploads and investigated files that remained queued.
- **Application maintenance:** Performed guided server-side Nextcloud updates and checked application behavior afterward.
- **Troubleshooting:** Investigated mobile app login/connectivity differences, new-device onboarding, upload behavior, and a WebDAV HTTP 423 locked-file error.

## Simplified architecture

```text
Authorized phone or laptop
          |
     Tailscale
          |
 Nexus (Ubuntu Server)
          |
      Docker
          |
  Nextcloud service ---- Host storage
          |
  Supporting service containers observed:
  MariaDB and Redis (exact integration pending verification)
```

This is a logical sketch of the access path, not a complete physical network diagram or a security certification. I have intentionally left out live endpoints and private account details.

## Observed infrastructure

| Component | Role / observation |
| --- | --- |
| Ubuntu Server | Host operating system for Nexus |
| Docker | Hosts the Nextcloud application and other containers |
| Nextcloud | Files, accounts, mobile access, and photo uploads |
| Tailscale | Private remote-access path used by approved devices |
| MariaDB, Redis | Container images observed running; precise dependencies to be documented |
| Mounted host storage | Separate disks/volumes exist; exact Nextcloud data path still being verified |

## Troubleshooting experience

| Issue encountered | Approach / learning | Documentation status |
| --- | --- | --- |
| Browser login worked while mobile app login failed | Compared Tailscale connectivity and browser behavior to isolate a client-specific issue | Exact resolution steps to be added |
| Phone photos remained waiting to upload | Investigated upload state and checked whether test files appeared on the service | End-to-end test evidence to be added |
| New iPhone needed to reconnect | Worked through approved device access and Nextcloud authentication flow | Repeatable onboarding guide planned |
| WebDAV HTTP 423 locked-file error | Recognized application-level file-lock behavior rather than assuming basic IP connectivity was broken | Root cause and confirmed fix not yet documented |
| Nextcloud update | Used the server-side application maintenance path with guidance | Version history and post-update tests to be added |

## Skills this project helps me practice

- Linux application administration and Docker service management
- Network connectivity and secure remote-access concepts
- Client troubleshooting and user account support
- Understanding the difference between application access, authentication, and file transfers
- Recording accurate evidence and validating changes

## Validation and limitations

I have used the service with approved users and tested access and file/photo upload workflows. However, this README does **not** claim that every security control has been audited, that all storage paths are verified, or that Nextcloud backups have passed a restore test. Successful Proxmox container backups elsewhere in my lab do not by themselves establish recoverability of Nextcloud's data and database.

## Planned improvements

- [ ] Capture sanitized screenshots of the application and a successful test upload.
- [ ] Identify the exact Nextcloud container names, network dependencies, and database connections.
- [ ] Verify the Nextcloud data directory and mounted storage volumes.
- [ ] Document access control and exposure checks without publishing private endpoints.
- [ ] Perform and document a tested Nextcloud backup and restore, including the database.
- [ ] Write up a troubleshooting incident with commands, root cause, and confirmed resolution.

## Attribution

This project was deployed, maintained, and troubleshot through **guided hands-on work**. I use technical assistance while learning and do not claim unsupported independent design, enterprise security, or production-grade disaster recovery.

**Privacy:** No credentials, user photos/files, personal account data, API keys, authentication tokens, or live service URLs are shared here.
