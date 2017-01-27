# Automatic Security Updates Role for Ansible

[![Build Status](https://travis-ci.org/petemcw/ansible-role-security-updates.svg?branch=master)](https://travis-ci.org/petemcw/ansible-role-security-updates)

Using this role install and setup automatic updates for Debian and RedHat families, to periodically install security upgrades. On Debian/Ubuntu the `unattended-upgrades` package is used and RedHat/CentOS uses `yum-cron`.

## Role Variables

The variables that can be passed to this role and a brief description about
them are as follows:

```yaml
# Enable automatic updates
security_updates_enabled: true

# An array of origins patterns to determine whether the package can be automatically installed
security_updates_apt_origins_patterns: []

# Packages which won't be automatically upgraded
security_updates_apt_package_blacklist: []

# Whether to attempt a recover on unclean dpkg exit
security_updates_apt_autofix_interrupted_dpkg: true

# Split the upgrade into the smallest possible chunks so that they can be interrupted with SIGUSR1
security_updates_apt_minimal_steps: false

# Install all unattended-upgrades when the machine is shutting down
security_updates_apt_install_on_shutdown: false

# Send information about upgrades or problems with unattended upgrades
security_updates_apt_mail: false

# E-mail address to send information about upgrades or problems with unattended upgrades
security_updates_apt_mail_address: "root@localhost"

# Send e-mail only on errors, otherwise e-mail will be sent every time there's a package upgrade
security_updates_apt_mail_only_on_error: false

# Do automatic removal of new unused dependencies after the upgrade
security_updates_apt_remove_unused_dependencies: false

# Automatically reboot system if any upgraded package requires it, immediately after the upgrade
security_updates_apt_automatic_reboot: false

# Automatically reboot system if any upgraded package requires it, at the specific time (HH:MM) instead of immediately after the upgrade
security_updates_apt_automatic_reboot_time: false

# Won't automatically upgrade some critical packages requiring restart after an upgrade, this forces it
security_updates_apt_ignore_apps_require_restart: false

# Only allocate certain amount of bandwidth for updates
security_updates_apt_dl_limit: 70

# Type of packages to update:
# default
# security
# security-severity:critical
# minimal
# minimal-security
# minimal-security-severity:critical
security_updates_yum_update_cmd: "security"

# Whether a message should be emitted when updates are available
security_updates_yum_update_messages: "yes"

# Whether updates should be downloaded when they are available
security_updates_yum_download_updates: "yes"

# Whether updates should be applied when they are available; download must also be "yes" for updates to be applied
security_updates_yum_apply_updates: "false"

# Maximum amout of time to randomly sleep, in minutes
security_updates_yum_random_sleep: 360

# Name to use for this system in messages that are emitted
security_updates_yum_system_name: "None"

# How to send messages.  Valid options are `stdio` and `email`
security_updates_yum_emit_via: "stdio"

# The width, in characters, that messages that are emitted should be formatted
security_updates_yum_output_width: 80

# The address to send email messages from
security_updates_yum_email_from: "root@localhost"

# List of addresses to send messages to
security_updates_yum_email_to: "root"

# Name of the host to connect to to send email messages
security_updates_yum_email_host: "localhost"

# List of groups to update
security_updates_yum_group_list: "None"

# The types of group packages to install
security_updates_yum_group_package_types:
  - mandatory
  - default

# Use this to filter Yum core messages
# -4: critical
# -3: critical+errors
# -2: critical+errors+warnings
security_updates_yum_debuglevel: -2

security_updates_yum_mdpolicy: "group:main"
```

## Examples

1. Configure the security updates with the defaults:

    ```yaml
    ---
    # This playbook configures automatic security updates

    - name: Configure security updates on all nodes
      hosts: all
      roles:
        - security-updates
    ```

## Dependencies

None.

## License

MIT
