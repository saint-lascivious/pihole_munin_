# pihole_munin_

Munin plugins for monitoring various Pi-hole® ≥ 6.0 statistics.

# Quick Start

## Step One: Download
* Download pihole_munin_
```
curl -sSL https://raw.githubusercontent.com/saint-lascivious/pihole_munin_/refs/heads/master/pihole_munin_ -o pihole_munin_ && chmod +x pihole_munin_
```

## Step Two: Install
* Install pihole_munin_
```
./pihole_munin_ install
```

## Step Three: …Wait
* Wait, around five minutes

Munin nodes run their plugins periodically, by default at 5 minute intervals past the hour.

# Documentation
## Plugins
```
  cache                Shows Pi-hole's cache
  cache_by_type        Shows Pi-hole's cached records by type
  clients              Shows active and total Pi-hole clients
  dnsmasq              Shows various Pi-hole FTLDNS dnsmasq statistics
  domains              Shows the number of domains being blocked by Pi-hole
  gravity              Shows various Pi-hole gravity database statistics
  percent              Shows Pi-hole's blocked query percentage
  privacy              Shows Pi-hole's privacy level
  queries              Shows Pi-hole queries
  queries_by_status    Shows Pi-hole queries by status
  queries_by_type      Shows Pi-hole queries by record type
  replies              Shows Pi-hole replies
  replies_by_type      Shows Pi-hole replies by record type
  status               Shows Pi-hole's blocking status
```

## Configuration
Example configuration for /etc/munin/plugin-conf.d/pihole_munin_

```
  [pihole_munin_*]
    ### AUTHENTICATION ###

    # The path at which Pi-hole's CLI password may be found.
    env.cli_password /etc/pihole/cli_pw

    # An application specific password will take precedence over a CLI
    # password if one is found to exist.
    #env.app_password APP_PASSWORD_HERE

    ### API ###

    # These variables are used to construct the base of the API URL.
    env.proto http
    env.host 127.0.0.1
    env.port 80
    env.api /api

    ### ALERTS ###

    # clients
    env.clients_active_crit 100
    env.clients_active_warn 1:50
    env.clients_total_crit 0:200
    env.clients_total_warn 100

    # domains
    env.domains_being_blocked_crit 1:5000000
    env.domains_being_blocked_warn 0:2500000

    # percent
    env.percent_blocked_crit 90
    env.percent_blocked_warn 1:75

    # privacy
    env.privacy_level_crit 1:3
    env.privacy_level_warn 3:3

    # queries
    env.queries_unique_domains_crit 1:20000
    env.queries_unique_domains_warn 0:10000

    # status
    env.status_crit 0:1
    env.status_warn 1:1

    ### MISCELLANEOUS ###

    # The user these plugins should run as.
    # The pihole user has access to the CLI password by default.
    user pihole

    # The graph_category value determines the category in which the
    # pihole_munin_* graphs appear in Munin's interface.
    env.graph_category dns

    # API responses are cached to reduce the number of requests made to the
    # Pi-hole API. This variable determines the time (in seconds) before
    # cached responses are considered stale.
    env.state_ttl 120
```

The plugin can be configured manually, or via the command line using the `admin` command.

E.g.
```
s@int:~$ sudo /usr/share/munin/plugins/pihole_munin_ admin add <var> <val>
s@int:~$ sudo /usr/share/munin/plugins/pihole_munin_ admin remove <var>
s@int:~$ sudo /usr/share/munin/plugins/pihole_munin_ admin list
```

Variables should be entered without the env. prefix, and values without quotes. Spaces in values are acceptable.

E.g.
```
    s@int:~$ sudo /usr/share/munin/plugins/pihole_munin_ admin add graph_category dns
    s@int:~$ sudo /usr/share/munin/plugins/pihole_munin_ admin add clients_active_warn 1:50
    s@int:~$ sudo /usr/share/munin/plugins/pihole_munin_ admin add clients_total_warn 100
```

* Usage
Link this plugin to /etc/munin/plugins/ as the desired plugin and restart the munin-node.

E.g.
```
  s@int:~$ sudo mv pihole_munin_ /usr/share/munin/plugins/pihole_munin_
  s@int:~$ sudo chmod +x /usr/share/munin/plugins/pihole_munin_
  s@int:~$ sudo ln -s /usr/share/munin/plugins/pihole_munin_ \
  /etc/munin/plugins/pihole_munin_blocked
  s@int:~$ sudo ln -s /usr/share/munin/plugins/pihole_munin_ \
  /etc/munin/plugins/pihole_munin_cache
```
etc.

Alternatively, you can use the 'admin' command to install all plugins at once.

E.g.
```
  s@int:~$ sudo /usr/share/munin/plugins/pihole_munin_ admin install
```

Or install or uninstall a a single plugin or group of plugins.

E.g.
```
  s@int:~$ sudo /usr/share/munin/plugins/pihole_munin_ admin install cache
  s@int:~$ sudo /usr/share/munin/plugins/pihole_munin_ admin uninstall cache cache_by_type
```

# Plugin Gallery
## cache
<picture>
  <img alt="This plugin shows Pi-hole's cache" src="https://github.com/saint-lascivious/pihole_munin_/blob/master/images/pihole_munin_cache-day.png">
</picture>

## cache_by_type
<picture>
  <img alt="This plugin shows Pi-hole's cached records by type" src="https://github.com/saint-lascivious/pihole_munin_/blob/master/images/pihole_munin_cache_by_type-day.png">
</picture>

## clients
<picture>
  <img alt="This plugin shows active and total Pi-hole clients" src="https://github.com/saint-lascivious/pihole_munin_/blob/master/images/pihole_munin_clients-day.png">
</picture>

## dnsmasq
<picture>
  <img alt="This plugin shows various Pi-hole FTLDNS dnsmasq statistics" src="https://github.com/saint-lascivious/pihole_munin_/blob/master/images/pihole_munin_dnsmasq-day.png">
</picture>

## domains
<picture>
  <img alt="This plugin shows the number of domains being blocked by Pi-hole" src="https://github.com/saint-lascivious/pihole_munin_/blob/master/images/pihole_munin_domains-day.png">
</picture>

## gravity
<picture>
  <img alt="This plugin shows various Pi-hole gravity database statistics" src="https://github.com/saint-lascivious/pihole_munin_/blob/master/images/pihole_munin_gravity-day.png">
</picture>

## percent
<picture>
  <img alt="This plugin shows Pi-hole's blocked query percentage" src="https://github.com/saint-lascivious/pihole_munin_/blob/master/images/pihole_munin_percent-day.png">
</picture>

## privacy
<picture>
  <img alt="This plugin shows Pi-hole's privacy level" src="https://github.com/saint-lascivious/pihole_munin_/blob/master/images/pihole_munin_privacy-day.png">
</picture>

## queries
<picture>
  <img alt="This plugin shows Pi-hole queries" src="https://github.com/saint-lascivious/pihole_munin_/blob/master/images/pihole_munin_queries-day.png">
</picture>

## queries_by_status
<picture>
  <img alt="This plugin shows Pi-hole queries by status" src="https://github.com/saint-lascivious/pihole_munin_/blob/master/images/pihole_munin_queries_by_status-day.png">
</picture>

## queries_by_type
<picture>
  <img alt="This plugin shows Pi-hole queries by record type" src="https://github.com/saint-lascivious/pihole_munin_/blob/master/images/pihole_munin_queries_by_type-day.png">
</picture>

## replies
<picture>
  <img alt="This plugin shows Pi-hole replies" src="https://github.com/saint-lascivious/pihole_munin_/blob/master/images/pihole_munin_replies-day.png">
</picture>

## replies_by_type
<picture>
  <img alt="This plugin shows Pi-hole replies by record type" src="https://github.com/saint-lascivious/pihole_munin_/blob/master/images/pihole_munin_replies_by_type-day.png">
</picture>

## status
<picture>
  <img alt="This plugin shows Pi-hole's blocking status" src="https://github.com/saint-lascivious/pihole_munin_/blob/master/images/pihole_munin_status-day.png">
</picture>

<p align="right"><sup><sub>pihole_munin_ - saint-lascivious (Hayden Pearce), ©2025</sub></sup></p>