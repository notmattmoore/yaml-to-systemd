# `yaml-to-systemd`

Create and set up systemd timers and services as described in a (terse) YAML
file.

I find systemd services and timers to be quite cumbersome compared to a
traditional cronfile. This script was written to enable a specification of
timers and services in a single YAML file.

Defaults and shortcuts are defined in `yaml-to-systemd` and can be set in the
YAML file as well. The relevant keys are described below.

| Key                | Description                                                                                                                                                                          |
| ---                | ---                                                                                                                                                                                  |
| `shortcuts`        | A dictionary. For each `(key, value)` pair, `key` will be replaced with `value` in unit file fields.                                                                                 |
| `exec_pre`         | String to prepend to non-absolute Exec... lines. Can be used to support aliases, etc. See `user-exec` in `.config/systemd/` in (dotfiles)[https://github.com/notmattmoore/dotfiles]. |
| `timer_defaults`   | A dictionary. Default field entries for `.timer` files.                                                                                                                              |
| `service_defaults` | A dictionary. Default field entries for `.service` files.                                                                                                                            |
| `unit_header`      | String to put at the top of unit files.                                                                                                                                              |
| `systemd_dir`      | `systemd` unit file directory. Typically `/etc/systemd/system` for systemd-mode and `~/.config/systemd/user` for user-mode.                                                          |
| `systemctl_cmd`    | Command to use for `systemctl`.                                                                                                                                                      |
| `dry_run`          | Whether to perform a dry-run.                                                                                                                                                        |

Keys `shortcuts`, `timer_defaults`, and `service_defaults` extend the defaults
in `yaml-to-systemd` while keys `exec_pre`, `unit_header`, `systemd_dir`,
`systemctl_cmd`, and `dry_run` override them.

Time specification is given in man systemd.time.

All top-level keys support array assignment, in which case the block is
*-expanded. For example, `{a: [b, c], d: e}` yields `{a:b, d:e}` and `{a:c,
d:e}`.

See the example files `cronfile-example-user.yaml` and
`cronfile-example-system.yaml`.
