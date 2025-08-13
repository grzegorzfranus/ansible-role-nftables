# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

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
