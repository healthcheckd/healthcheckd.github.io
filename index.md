---
layout: home
title: healthcheckd - Health check daemon for AWS ALB/NLB
---
healthcheckd is a lightweight health check daemon designed for AWS Application
and Network Load Balancers. It runs configurable checks (disk, file, HTTP, TCP,
systemd units, and arbitrary commands) and exposes results via an HTTP endpoint
with Prometheus metrics.

## How to Install?

### Individually

Get the latest release from [healthcheckd/healthcheckd](
https://github.com/healthcheckd/healthcheckd/releases/latest)

### Add a Debian Repository

Download the [public key](healthcheckd.asc) and add it to your apt keyring:

```
wget -qO- {{ site.url }}/healthcheckd.asc | sudo tee /etc/apt/keyrings/healthcheckd.asc >/dev/null
```

Next, create the source in `/etc/apt/sources.list.d/`:

```
echo "deb [arch=amd64 signed-by=/etc/apt/keyrings/healthcheckd.asc] {{ site.url }}/deb stable main" | sudo tee /etc/apt/sources.list.d/healthcheckd.list >/dev/null
```

Then run `apt update && apt install -y healthcheckd`.

### Add a RPM Repository

Download the repo file:

```
cd /etc/yum.repos.d ; curl {{ site.url }}/healthcheckd.repo -LO
```

Then run `yum install -y healthcheckd`.

## After installing

Configure your checks in `/etc/healthcheckd/config.d/` (see the included
`example.yaml` for reference) and then run:

```
systemctl enable --now healthcheckd.service
```

The daemon listens on port 9990 by default. Edit `/etc/healthcheckd/config` to
change the bind address, port, check frequency, or log level.

## How to contribute?

Please contribute changes and bug reports in the
[healthcheckd repository](https://github.com/healthcheckd/healthcheckd).

Have a security issue? Please email [Jon](mailto:jon@sprig.gs) with details.
