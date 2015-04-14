# unattended\_upgrades


## Overview

The unattended\_upgrades module allows for the installation and configuration of automatic security (and other) updates through apt.

This functionality used to be part of the puppetlabs-apt module but was split off into its own module.

## Module Description

The unattended\_upgrades module automates the configuration of apt package updates.

## Setup

### What unattended\_upgrades affects:

* Package/configuration for unattended\_upgrades

### Beginning with unattended\_upgrades

All you need to do is include the module `include unattended_upgrades`.

## Usage

Using unattended\_upgrades simply consists of including the module and if needed altering some of the default settings.

## Reference

### Classes

* `unattended_upgrades`: Main class, installs the necessary packages and writes the configuration.

### Parameters

#### unattended\_upgrades

* `auto`: A hash of settings with three possible keys:
  * `fix_interrupted_dpkg`(`true`): Try to fix package installation state
  * `reboot`(`false`): Reboot system after package update installation
  * `remove`(`true`): Remove unneeded dependencies after update installation

  Any of these keys can be specified and will be merged into the defaults, so if you only want to   change the `reboot` behaviour the following is enough:

  ```puppet
  class { 'unattended_upgrades':
    auto => { 'reboot' => true },
  }
  ```
* `blacklist`(`[]`): A list of packages to **not** automatically upgrade. This list is empty by default.
* `dl_limit`(`undef`): Use a bandwidth limit for downloading, specified in kb/sec.
* `enable` (`1`): Enable the automatic installation of updates.
* `install_on_shutdown` (`false`): Install updates on shutdown instead of in the background.
* `legacy_origin` (`false`): Use the legacy `Unattended-Upgrade::Allowed-Origins` setting or the modern `Unattended-Upgrade::Origins-Pattern`.
* `mail`: A hash to configure email behaviour. The possible keys are:
  * `only_on_error` (`true`): Only send mail when something went wrong
  * `to` (`undef`): Email address to send email too

  If the default for `to` is kept you will not receive any mail at all. You'll likely want to set this parameter:

  ```puppet
  class { 'unattended_upgrades':
    mail => { 'to' => 'admin@domain.tld', },
  }
  ```
* `minimal_steps` (`true`): Split the upgrade process into sections to allow shutdown during upgrade.
* `origins`: The repositories from which to automatically upgrade included packages.
* `package_ensure` (`installed`): The ensure state for the 'unattended-upgrades' package.


## Limitations

This module should work across all versions of Debian/Ubuntu.

## License

The original code for this module comes from Evolving Web and was licensed under the MIT license. Code added since the fork of that module into puppetlabs-apt is covered under the Apache License version 2 as is any code added since it was split off into this separate unattended\_upgrades module.

The LICENSE contains both licenses.
