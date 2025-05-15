# pihole_munin_
<p align="center">
    <img src="https://raw.githubusercontent.com/wiki/saint-lascivious/pihole_munin_/images/misc/epic_handshake_.png" alt="Munin plugins for monitoring various Pi-hole® ≥ 6.0 statistics."/>
</p>

[Munin](https://munin-monitoring.org) [plugins](https://gallery.munin-monitoring.org) for monitoring various [Pi-hole®](https://github.com/pi-hole/pi-hole) ≥ 6.0 statistics.

---

## Overview

`pihole_munin_` is a POSIX shell script that acts as a wildcard Munin plugin, providing a suite of metrics for Pi-hole installations. It supports dynamic configuration, authentication, plugin management, and state caching.

---

## Features

- **Supported Metrics:**
  - Cache statistics (total, evicted, expired, immortal, inserted)
  - Cache by type (valid/stale per record type)
  - Client statistics (active, total)
  - DNSMasq/FTLDNS statistics
  - Domains being blocked
  - Gravity database stats (groups, adlists, allowed/blocked domains/regex)
  - Percent blocked
  - Privacy level
  - Query statistics (blocked, cached, forwarded, total, unique domains, frequency)
  - Queries by status/type
  - Replies/by type
  - Blocking status
- **Alert Thresholds** Configurable warning and critical thresholds for metrics.
- **Authentication:** Supports Pi-hole app password, web password, or CLI password (auto-detected).
- **State Caching:** Reduces API calls by caching responses.
- **Session Caching:** Optionally reuses API sessions.
- **Admin Commands:** Enable/disable plugins, manage config, update and more.
- **Wildcard Plugin:** Single script, multiple metrics via symlinks.
- **Munin Capabilities:** Supports autoconf, suggest, dirtyconfig, fetch and config.
- **POSIX Only:** No bashisms, no shellcheck ignore directives.

---

## Installation

### Automatic

```sh
./pihole_munin_ admin enable
```

### Manual

```sh
sudo mv pihole_munin_ /usr/share/munin/plugins/pihole_munin_
sudo chmod +x /usr/share/munin/plugins/pihole_munin_
sudo ln -s /usr/share/munin/plugins/pihole_munin_ /etc/munin/plugins/pihole_munin_cache
# ...repeat for other plugins as needed
sudo systemctl restart munin-node.service
```

---

## Configuration

Example `/etc/munin/plugin-conf.d/pihole_munin_` file:

```ini
[pihole_munin_*]
    env.cli_password /etc/pihole/cli_pw
    env.proto http
    env.host 127.0.0.1
    env.port 80
    env.api /api
    env.graph_category dns
    env.state_ttl 120
    env.session_ttl 300
    user pihole
```

---

## Usage

### Fetch Data

Munin will call the plugin with the appropriate symlink name, e.g.:

```sh
/usr/share/munin/plugins/pihole_munin_cache fetch
```

### Admin Commands

- Enable all plugins:  
  `./pihole_munin_ admin enable`
- Disable all plugins:  
  `./pihole_munin_ admin disable`
- Add config variable:  
  `./pihole_munin_ admin add <var> [value]`
- Remove config variable:  
  `./pihole_munin_ admin remove <var>`
- List config variables:  
  `./pihole_munin_ admin list`
- Update plugin:  
  `./pihole_munin_ admin update`

---

## Authentication

Order of precedence:
1. `env.app_password`
2. `env.pihole_password`
3. `env.cli_password` (if host is localhost)

---

## Dependencies

- `curl`
- `jq`

---

## Documentation
Documentation for `pihole_munin_` can be found in [the pihole_munin_ wiki](https://github.com/saint-lascivious/pihole_munin_/wiki#pihole_munin_).

---

## **Compatibility**
- **Pi-hole Version** Compatible with Pi-hole >= 6.0.
- **Munin Version** Compatible with Munin >= 2.0.49.

---

## See Also

- [Munin](https://munin-monitoring.org)
- [Pi-hole](https://github.com/pi-hole/pi-hole)
- [Munin Plugins](https://gallery.munin-monitoring.org)

---

<p align="right"><sup><sub>© 2025, saint-lascivious (Hayden Pearce)</sub></sup></p>
