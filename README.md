# oci-prometheus-sd-proxy TUF-on-CI Signing Repository

[![Docker Image](https://img.shields.io/badge/Docker-ghcr.io-blue?logo=docker)](https://github.com/amaanx86/oci-prometheus-sd-proxy/pkgs/container/oci-prometheus-sd-proxy)
[![OpenSSF Best Practices](https://www.bestpractices.dev/projects/12388/badge)](https://www.bestpractices.dev/projects/12388)
[![SLSA 3](https://slsa.dev/images/gh-badge-level3.svg)](https://slsa.dev)
[![GitHub Release](https://img.shields.io/github/v/release/amaanx86/oci-prometheus-sd-proxy)](https://github.com/amaanx86/oci-prometheus-sd-proxy/releases)

<img width="469" height="277" alt="OCI Prometheus SD Proxy" src="https://github.com/user-attachments/assets/333a7c32-93bd-4ad9-aea3-aea2d6a66a65" />

This repository holds the [TUF-on-CI](https://github.com/theupdateframework/tuf-on-ci) signing infrastructure for [oci-prometheus-sd-proxy](https://github.com/amaanx86/oci-prometheus-sd-proxy).

- **Main repo**: https://github.com/amaanx86/oci-prometheus-sd-proxy
- **Documentation**: https://oci-prometheus-sd-proxy.readthedocs.io/
- **Release docs**: https://oci-prometheus-sd-proxy.readthedocs.io/en/latest/releasing.html

---

## Overview

TUF-on-CI automates [The Update Framework (TUF)](https://theupdateframework.io/) metadata management using GitHub Actions. When a new release is published, maintainers sign the targets metadata using their GitHub identity via Sigstore - no private key material is stored or shared.

---

## Setup

### 1. Clone this repository

```bash
git clone https://github.com/amaanx86/oci-prometheus-sd-proxy-tuf-on-ci.git
cd oci-prometheus-sd-proxy-tuf-on-ci
```

### 2. Create and activate a Python virtual environment

```bash
python3 -m venv .venv-tuf
source .venv-tuf/bin/activate
```

> On Windows use `.venv-tuf\Scripts\activate`

### 3. Install tuf-on-ci

```bash
pip3 install tuf-on-ci-sign
```

### 4. Configure the signing tool

The `.tuf-on-ci-sign.ini` file in the repository root configures your local signing environment:

```ini
[settings]
user-name = @amaanx86
pull-remote = origin
push-remote = origin
pykcs11lib = /opt/homebrew/lib/libykcs11.dylib
```

Update `user-name` to your GitHub username (with the `@` prefix) if you are a new maintainer. The `pykcs11lib` path is only required if you use a hardware token (e.g. YubiKey); remove it if signing with Sigstore browser flow only.
