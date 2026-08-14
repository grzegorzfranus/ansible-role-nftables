# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

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
