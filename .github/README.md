# pihole_munin_
<p align="center">
    <img src="https://raw.githubusercontent.com/wiki/saint-lascivious/pihole_munin_/images/misc/epic_handshake_.png" alt="Munin plugins for monitoring various Pi-hole® ≥ 6.0 statistics."/>
</p>

[Munin](https://munin-monitoring.org) [plugins](https://gallery.munin-monitoring.org) for monitoring various [Pi-hole®](https://github.com/pi-hole/pi-hole) ≥ 6.0 statistics.

---

## Overview
`pihole_munin_` is a Munin plugin designed to monitor and visualize various Pi-hole statistics. It provides detailed insights into Pi-hole's performance, usage, and configuration through Munin's graphing interface.

---

## Key Features

### **Supported Metrics**
- **Cache Statistics**
  - Total cached records
  - Evicted, expired, immortal, and inserted records
- **Client Statistics**
  - Active and total clients
- **DNS Statistics**
  - Queries by type (e.g., A, AAAA, PTR)
  - Queries by status (e.g., blocked, forwarded)
  - Replies by type
- **Gravity Database**
  - Blocked domains, allowed domains, regex rules
  - Adlists and group counts
- **Blocking Status**
  - Enabled/disabled state
- **Privacy Level**
  - Current privacy configuration
- **Query Statistics**
  - Total, blocked, cached, forwarded queries
  - Unique domains queried
  - Query frequency (queries per second)
- **Percent Blocked**
  - Percentage of queries blocked

---

### **Plugin Management**
- **Wildcard Plugin Support**
  - Single script handles multiple metrics via symbolic links.
- **Automatic Installation**
  - Command to install and enable all plugins at once.
- **Dynamic Configuration**
  - Easily configure thresholds, API settings, and more via the command line.

---

### **Authentication/API**
- Supports multiple authentication methods:
  - Pi-hole application password
  - Pi-hole web interface password
  - CLI password (auto-detected if available)
- State files:
  - Store the last known state of each metric.
  - Automatically update state files to avoid unnecessary API calls.
- Optional session cache:
  - Force all plugins to use the same session, if that's a thing you want to do, for reasons.

---

### **Customization**
- **Alert Thresholds**
  - Configure warning and critical thresholds for metrics.
- **Graph Categories**
  - Organize graphs under custom categories in Munin.
- **API Configuration**
  - Flexible API endpoint and protocol settings.

---

### **Admin Commands**
- **Enable/Disable Plugins**
  - Enable or disable `pihole_munin_` plugins.
- **Configuration Management**
  - Add, remove, or list configuration variables.
- **Update**
  - Automatically fetch and install the latest version of the plugin.

---

### **Compatibility**
- **Pi-hole Version**
  - Compatible with Pi-hole >= 6.0.
- **Munin Version**
  - Compatible with Munin >= 2.0.49.
- **Dependencies**
  - Requires `curl` and `jq` for API interaction.
- **Language**
  - Written entirely in POSIX `shell`, you'll find no [shellcheck](https://github.com/koalaman/shellcheck) [ignore directives](https://github.com/koalaman/shellcheck/wiki/Ignore) here.
  - I don't care if shell X, Y or Z supports `local` variables, `bash` arrays, or any other non-POSIX feature. This is a POSIX shell script, and it will remain that way.

---

## Example Usage
```sh
# Enable all plugins
./pihole_munin_ admin enable

# Add a configuration variable
./pihole_munin_ admin add graph_category dns
```

---

## Documentation
Documentation for `pihole_munin_` can be found in [the pihole_munin_ wiki](https://github.com/saint-lascivious/pihole_munin_/wiki#pihole_munin_).

---

<p align="right"><sup><sub>© 2025, saint-lascivious (Hayden Pearce)</sub></sup></p>
