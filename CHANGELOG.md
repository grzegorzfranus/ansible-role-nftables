# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [2.1.5](https://github.com/grzegorzfranus/ansible-role-nftables/compare/v2.1.4...v2.1.5) (2026-08-16)


### Bug Fixes

* **defaults:** use RFC 5737 documentation addresses in examples ([#38](https://github.com/grzegorzfranus/ansible-role-nftables/issues/38)) ([#39](https://github.com/grzegorzfranus/ansible-role-nftables/issues/39)) ([55d71bd](https://github.com/grzegorzfranus/ansible-role-nftables/commit/55d71bdf7abac456df3d394944e5fb0ea7cffebf))

## [2.1.4](https://github.com/grzegorzfranus/ansible-role-nftables/compare/v2.1.3...v2.1.4) (2026-08-16)


### Code Refactoring

* **vars:** prefix internal variables with double underscore ([#35](https://github.com/grzegorzfranus/ansible-role-nftables/issues/35)) ([#36](https://github.com/grzegorzfranus/ansible-role-nftables/issues/36)) ([e5210d3](https://github.com/grzegorzfranus/ansible-role-nftables/commit/e5210d3efa51c6c03340ee105f5fe21544e8a9fd))

## [2.1.3](https://github.com/grzegorzfranus/ansible-role-nftables/compare/v2.1.2...v2.1.3) (2026-08-16)


### Bug Fixes

* **tasks:** add explicit states, template backups and logrotate validation ([#32](https://github.com/grzegorzfranus/ansible-role-nftables/issues/32)) ([#33](https://github.com/grzegorzfranus/ansible-role-nftables/issues/33)) ([7604609](https://github.com/grzegorzfranus/ansible-role-nftables/commit/7604609562bb5fd67e2143b386dc6b8b4ce5931e))

## [2.1.2](https://github.com/grzegorzfranus/ansible-role-nftables/compare/v2.1.1...v2.1.2) (2026-08-16)


### Bug Fixes

* **templates:** render valid matchers for protocol-only and NAT rules ([#29](https://github.com/grzegorzfranus/ansible-role-nftables/issues/29)) ([#30](https://github.com/grzegorzfranus/ansible-role-nftables/issues/30)) ([41fb172](https://github.com/grzegorzfranus/ansible-role-nftables/commit/41fb17290b12451c8205b3651426115795ca5d65))

## [2.1.1](https://github.com/grzegorzfranus/ansible-role-nftables/compare/v2.1.0...v2.1.1) (2026-08-16)


### Bug Fixes

* **reboot:** remove spurious reboot trigger and namespace reboot variables ([#26](https://github.com/grzegorzfranus/ansible-role-nftables/issues/26)) ([#27](https://github.com/grzegorzfranus/ansible-role-nftables/issues/27)) ([70e0d6f](https://github.com/grzegorzfranus/ansible-role-nftables/commit/70e0d6f7bbd586499d0a43c481b974a8c1a90d9f))

## [2.1.0](https://github.com/grzegorzfranus/ansible-role-nftables/compare/v2.0.2...v2.1.0) (2026-08-16)


### Features

* **meta:** add declarative argument specifications ([#23](https://github.com/grzegorzfranus/ansible-role-nftables/issues/23)) ([#24](https://github.com/grzegorzfranus/ansible-role-nftables/issues/24)) ([dae8fdd](https://github.com/grzegorzfranus/ansible-role-nftables/commit/dae8fdd0270f0364533d2f1411dfc4e9817212cf))

## [2.0.2](https://github.com/grzegorzfranus/ansible-role-nftables/compare/v2.0.1...v2.0.2) (2026-08-16)


### Bug Fixes

* **rules:** stop dropping IPv6 traffic in inet filter table ([#20](https://github.com/grzegorzfranus/ansible-role-nftables/issues/20)) ([#21](https://github.com/grzegorzfranus/ansible-role-nftables/issues/21)) ([1a06fc4](https://github.com/grzegorzfranus/ansible-role-nftables/commit/1a06fc48d5d64a3dd24e2ca9e80e90e8768d1b8a))

## [2.0.1](https://github.com/grzegorzfranus/ansible-role-nftables/compare/v2.0.0...v2.0.1) (2026-08-16)


### Bug Fixes

* **assert:** remove always-true guards from variable validation ([#17](https://github.com/grzegorzfranus/ansible-role-nftables/issues/17)) ([#18](https://github.com/grzegorzfranus/ansible-role-nftables/issues/18)) ([56063ac](https://github.com/grzegorzfranus/ansible-role-nftables/commit/56063ac9dd37fcf8c1870c0955d0e1702703560f))

## [2.0.0](https://github.com/grzegorzfranus/ansible-role-nftables/compare/v1.7.2...v2.0.0) (2026-08-15)


### ⚠ BREAKING CHANGES

* **tasks:** drive execution with prefixed tags instead of nftables_role_action ([#14](https://github.com/grzegorzfranus/ansible-role-nftables/issues/14)) (#15)

### Code Refactoring

* **tasks:** drive execution with prefixed tags instead of nftables_role_action ([#14](https://github.com/grzegorzfranus/ansible-role-nftables/issues/14)) ([#15](https://github.com/grzegorzfranus/ansible-role-nftables/issues/15)) ([1ca34d5](https://github.com/grzegorzfranus/ansible-role-nftables/commit/1ca34d54880ce286dba2b3818823adc502663769))

## [1.7.2](https://github.com/grzegorzfranus/ansible-role-nftables/compare/v1.7.1...v1.7.2) (2026-08-15)


### Bug Fixes

* correct NAT rule rendering for logging and inet tables ([#12](https://github.com/grzegorzfranus/ansible-role-nftables/issues/12)) ([514608e](https://github.com/grzegorzfranus/ansible-role-nftables/commit/514608e124edea0fa91b8f6dc5381e0c81fe7b3f))

## [1.7.1](https://github.com/grzegorzfranus/ansible-role-nftables/compare/v1.7.0...v1.7.1) (2026-08-15)


### CI/CD

* restore yamllint settings required by ansible-lint ([#8](https://github.com/grzegorzfranus/ansible-role-nftables/issues/8)) ([0b42565](https://github.com/grzegorzfranus/ansible-role-nftables/commit/0b4256589950df627a766f2c7f9d243f8ff458d5))

## [1.7.0](https://github.com/grzegorzfranus/ansible-role-nftables/compare/v1.6.0...v1.7.0) (2026-08-15)


### Features

* support interface matching in user-defined input and output rules ([#7](https://github.com/grzegorzfranus/ansible-role-nftables/issues/7)) ([2a1a045](https://github.com/grzegorzfranus/ansible-role-nftables/commit/2a1a04598b57d9283953a7721b8f6919f42744e7))

## [1.6.0](https://github.com/grzegorzfranus/ansible-role-nftables/compare/v1.5.2...v1.6.0) (2026-08-15)


### Features

* add docker-aware firewall mode ([#5](https://github.com/grzegorzfranus/ansible-role-nftables/issues/5)) ([3ecd3a5](https://github.com/grzegorzfranus/ansible-role-nftables/commit/3ecd3a56362e05e9324a8cf2e1580066e78703e1))

## [1.5.2](https://github.com/grzegorzfranus/ansible-role-nftables/compare/v1.5.1...v1.5.2) (2026-08-14)


### Documentation

* restructure README to standard section layout ([#3](https://github.com/grzegorzfranus/ansible-role-nftables/issues/3)) ([3803f0d](https://github.com/grzegorzfranus/ansible-role-nftables/commit/3803f0de15b96042aa43397fed0f00ff9af13c83))

## [1.5.1](https://github.com/grzegorzfranus/ansible-role-nftables/compare/v1.5.0...v1.5.1) (2026-08-14)


### CI/CD

* modernize repository automation and configs ([#1](https://github.com/grzegorzfranus/ansible-role-nftables/issues/1)) ([4a347dc](https://github.com/grzegorzfranus/ansible-role-nftables/commit/4a347dc79abab8f9ee744cdf1c4b249e067fecd8))

## [1.5.0] - 2025-11-30

### Fixed 🔧
- Fix Ansible 2.20 compatibility: assertion for user-defined rules counter field now returns proper boolean instead of string from regex match
- Update conditional logic in `assert.yml` to use `select('equalto', 'bool')` pattern for type validation
- Fix Ansible 2.24 deprecation warnings: replace top-level fact variables with `ansible_facts['...']` format across all task files, handlers, and molecule tests

### Changed 🔄
- Remove emojis from all task and handler names for cleaner output and better log parsing
- Minimum Ansible version bumped to 2.20 compatibility

---

## [1.4.0] - 2025-08-13
### Added ✅
- CHANGELOG introduced and aligned with core rules.

### Changed 🔄
- Replace shell-based reboot with `ansible.builtin.reboot` and `wait_for_connection` using numeric defaults.
- Modernize ACL service restart to `ansible.builtin.service` and shorten pause.
- Fix handler notify name to match existing handler: `Restart nftables service`.
- Add emojis to all task and handler names for consistent, readable task output.
- Update assertion tasks to include clear success/failure messages and emojis, matching house style.
- README: align supported OS list with `meta/main.yml` (remove Oracle Linux).

### Fixed 🔧
- Ensure consistent handler names and Ansible builtins usage across tasks.
- Add listening handler aliases to match notify names after emoji changes.
- Fix nft rules validation when only `port` is provided by defaulting L4 protocol to `tcp` in `user_defined.rules.j2`.

### Removed ❌
- Async shell-based service restart in ACL block.

---

## [1.3.1] - 2024-01-01
### Added ✅
- Previous minor improvements and documentation updates.
