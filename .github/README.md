# pihole_munin_
<p align="center">
    <a href="https://github.com/saint-lascivious/pihole_munin_/wiki">
        <img src="https://raw.githubusercontent.com/wiki/saint-lascivious/pihole_munin_/images/misc/pihole_munin_.png"
             alt="Munin plugins for monitoring various Pi-hole® ≥ 6.0 statistics."
             style="max-width: 1000px; width: 100%; height: auto;" />
    </a>
</p>

[Munin](https://munin-monitoring.org) [plugins](https://gallery.munin-monitoring.org) for monitoring various [Pi-hole®](https://github.com/pi-hole/pi-hole) ≥ 6.0 statistics.

---

## Overview

`pihole_munin_` is a POSIX shell script that acts as a wildcard Munin plugin, providing a suite of metrics for Pi-hole installations. It supports dynamic configuration, authentication, plugin management, and state caching.

---

## Features

- **Comprehensive Pi-hole Metrics:**
  - Cache statistics (total, evicted, expired, immortal, inserted)
  - Cache breakdown by record type (valid/stale)
  - Client statistics (active, total)
  - DNSMasq/FTLDNS statistics
  - Domains currently being blocked
  - Gravity database stats (groups, adlists, allowed/blocked domains/regex)
  - Percent blocked
  - Privacy level
  - Query statistics (blocked, cached, forwarded, total, unique domains, frequency)
  - Queries by status/type
  - Replies by type
  - Blocking status

- **Configurable Alert Thresholds:**  
  Set warning and critical thresholds for key metrics to enable Munin alerting.

- **Flexible Authentication:**  
  Automatically detects and supports Pi-hole app password, web password, or CLI password.

- **Efficient State & Session Caching:**  
  Minimizes API calls by caching responses and optionally reusing API sessions for improved performance.

- **Powerful Admin Commands:**  
  Easily install, uninstall, update, enable/disable plugins, and manage configuration variables from the command line.

- **Wildcard Plugin Architecture:**  
  A single POSIX shell script provides multiple metrics via symlinks, simplifying deployment and updates.

- **Full Munin Integration:**  
  Supports all standard Munin plugin capabilities: `autoconf`, `suggest`, `dirtyconfig`, `fetch`, and `config`.

- **Strict POSIX Compliance:**  
  Written in 100% pure POSIX shell.

- **Progressive Verbosity for Troubleshooting:**  
  Built-in test mode with `--verbose` and `--trace` options for detailed plugin diagnostics and Munin debug output.

- **Extensive Configurability:**  
  Nearly every aspect of the plugin's behavior can be customized via environment variables, configuration files, or admin commands. Allowing you to tailor metrics, authentication, thresholds, caching, and more to your specific needs.

---

## Installation

### Automatic

```sh
./pihole_munin_ admin install
```

### Manual

```sh
sudo mv pihole_munin_ /usr/share/munin/plugins/pihole_munin_
sudo chmod +x /usr/share/munin/plugins/pihole_munin_
sudo ln -s /usr/share/munin/plugins/pihole_munin_ /etc/munin/plugins/pihole_munin_cache
sudo ln -s /usr/share/munin/plugins/pihole_munin_ /etc/munin/plugins/pihole_munin_cache_by_type
# ...repeat for other plugins as needed
sudo systemctl restart munin-node.service
```

The full list of plugins is:
`ccache`, `cache_by_type`, `clients`, `dnsmasq`, `domains`, `frequency`, `gravity`, `overview`, `percent`, `privacy`, `queries`, `queries_by_status`, `queries_by_type`, `replies` `replies_by_type`, `status` and `unique`.

---

## Configuration

Example `/etc/munin/plugin-conf.d/pihole_munin_` file:

```ini
# pihole_munin_ configuration for Munin
[pihole_munin_*]
    env.cli_password /etc/pihole/cli_pw
    env.proto http
    env.host 127.0.0.1
    env.port 80
    env.api /api
    env.graph_category dns
    env.state_ttl 240
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
  `./pihole_munin_ admin install`
- Disable all plugins:
  `./pihole_munin_ admin uninstall`
- Add config variable:
  `./pihole_munin_ admin add <var> [value]`
- Remove config variable:
  `./pihole_munin_ admin remove <var>`
- List config variables:
  `./pihole_munin_ admin list`
- Update plugin:
  `./pihole_munin_ admin update`
- Set password:
  `./pihole_munin_ admin password <password>`

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
- `mktemp`

---

## Documentation
Documentation for `pihole_munin_` can be found in [the pihole_munin_ wiki](https://github.com/saint-lascivious/pihole_munin_/wiki#pihole_munin_).

---

## **Compatibility**
- **Pi-hole Version** Compatible with Pi-hole >= 6.0.
- **Munin Version** Compatible with Munin >= 2.0.

---

## See Also

- [Munin](https://munin-monitoring.org)
- [Pi-hole](https://github.com/pi-hole/pi-hole)
- [Munin Plugins](https://gallery.munin-monitoring.org)

---

| ![home][home_icon] | ![install][install_icon] | ![config][config_icon] | ![update][update_icon] | ![help][help_icon] | ![uninstall][uninstall_icon] | ![discuss][discussions_icon] | ![bug][bug_report_icon] |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| [Home][home] | [Install][install] | [Configuration][configuration] | [Update][update] | [Help][help] | [Uninstall][uninstall] | [Discussions] | [Report A Bug] |

[home]: https://github.com/saint-lascivious/pihole_munin_/wiki/Home
[install]: https://github.com/saint-lascivious/pihole_munin_/wiki/Install
[configuration]: https://github.com/saint-lascivious/pihole_munin_/wiki/Configuration
[update]: https://github.com/saint-lascivious/pihole_munin_/wiki/Update
[help]: https://github.com/saint-lascivious/pihole_munin_/wiki/Help
[uninstall]: https://github.com/saint-lascivious/pihole_munin_/wiki/Uninstall
[Discussions]: https://github.com/saint-lascivious/pihole_munin_/discussions
[Report A Bug]: https://github.com/saint-lascivious/pihole_munin_/issues/new?assignees=saint-lascivious&labels=bug&template=BUG_REPORT.md&title=pihole_munin_%3A+bug+report

[home_icon]: https://raw.githubusercontent.com/wiki/saint-lascivious/pihole_munin_/images/icons/Home.png "Home page."
[install_icon]: https://raw.githubusercontent.com/wiki/saint-lascivious/pihole_munin_/images/icons/Install.png "Install pihole_munin_."
[config_icon]: https://raw.githubusercontent.com/wiki/saint-lascivious/pihole_munin_/images/icons/Configuration.png "Configure pihole_munin_."
[update_icon]: https://raw.githubusercontent.com/wiki/saint-lascivious/pihole_munin_/images/icons/Update.png "Update pihole_munin_."
[help_icon]: https://raw.githubusercontent.com/wiki/saint-lascivious/pihole_munin_/images/icons/Help.png "Get help with pihole_munin_."
[uninstall_icon]: https://raw.githubusercontent.com/wiki/saint-lascivious/pihole_munin_/images/icons/Uninstall.png "Uninstall pihole_munin_."
[discussions_icon]: https://raw.githubusercontent.com/wiki/saint-lascivious/pihole_munin_/images/icons/Discussions.png "Not sure if you have a bug or issue? Just want to say hello? Discuss pihole_munin_ using the GitHub Discussions platform."
[bug_report_icon]: https://raw.githubusercontent.com/wiki/saint-lascivious/pihole_munin_/images/icons/Bug_Report.png "Report a bug in pihole_munin_."

<p align="right"><sup><sub>© 2025, saint-lascivious (Hayden Pearce)</sub></sup></p>
