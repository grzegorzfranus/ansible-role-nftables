# Ansible Role: NFTables

|Source|Version|CI|License|
|------|-------|-------|-------|
|[![Source Code](https://img.shields.io/badge/source-github-blue.svg)](https://github.com/grzegorzfranus/ansible-role-nftables)|[![Version](https://img.shields.io/github/v/release/grzegorzfranus/ansible-role-nftables)](https://github.com/grzegorzfranus/ansible-role-nftables/releases)|[![tests](https://github.com/grzegorzfranus/ansible-role-nftables/actions/workflows/ci.yml/badge.svg)](https://github.com/grzegorzfranus/ansible-role-nftables/actions)|[![Repository License](https://img.shields.io/badge/license-apache2.0-brightgreen.svg)](LICENSE)|

This Ansible role installs and configures NFTables, a powerful and flexible firewall system for Linux. It provides a comprehensive solution for network packet filtering with features like stateful connection tracking, rate limiting, logging, and NAT.

## Main Actions

- Verify and handle system requirements
- Disable conflicting firewall services (firewalld, iptables, ufw)
- Install NFTables package
- Configure NFTables service
- Deploy base filtering rules
- Configure security protection rules (optional)
- Set up cluster communication rules (optional)
- Configure user-defined custom rules (optional)
- Configure NAT rules (optional)
- Set up logrotate for NFTables logs (optional)
- Upgrade NFTables package (when requested)

## Requirements

### Supported operating systems
List of officially supported operating systems:
| OS Family | Version | Status |
|-----------|---------|---------|
| Ubuntu | 24.04 (Noble) | ![✓](https://img.shields.io/badge/✓-brightgreen.svg) |
| Ubuntu | 22.04 (Jammy) | ![✓](https://img.shields.io/badge/✓-brightgreen.svg) |
| Debian | 12 (Bookworm) | ![✓](https://img.shields.io/badge/✓-brightgreen.svg) |
| Debian | 11 (Bullseye) | ![✓](https://img.shields.io/badge/✓-brightgreen.svg) |
| Rocky Linux | 9 | ![✓](https://img.shields.io/badge/✓-brightgreen.svg) |
| Oracle Linux | 9 | ![✓](https://img.shields.io/badge/✓-brightgreen.svg) |

### Ansible version

Ansible >= 2.15

### Python version

Python >= 3.9

### Setup module
The role uses facts gathered by Ansible on the remote host. If you disable the Setup module in your playbook, the role will not work properly.

### Root access
This role requires root access, so either configure it in your inventory files, run it in a playbook with a global `become: true` or invoke the role in your playbook like:
```yaml
- hosts: servers
  become: true
  roles:
    - role: grzegorzfranus.nftables
```

## Role Variables

### 1. General Settings

| Variable | Description | Default |
|----------|-------------|---------|
| `nftables_role_action` | Define which parts of the role to execute (Options: 'all', 'requirements', 'install', 'configure', 'rules', 'acl', 'logrotate', 'upgrade') | `"all"` |
| `nftables_service_enabled` | Enable/disable NFTables service on boot | `true` |
| `nftables_configure_logrotate` | Enable/disable logrotate configuration for NFTables logs | `true` |
| `nftables_configure_security_rules` | Enable/disable additional security protection rules | `false` |

### 2. Logging Configuration

| Variable | Description | Default |
|----------|-------------|---------|
| `nftables_logrotate_options` | Dictionary of logrotate settings | See below |
| `nftables_logrotate_options.archive_directory_path` | Directory where archived logs will be stored | `/var/log/nftables` |
| `nftables_logrotate_options.frequency` | How often to rotate logs | `"daily"` |
| `nftables_logrotate_options.count` | Number of rotated log files to keep | `90` |
| `nftables_logrotate_options.missingok` | Don't error if log file is missing | `true` |
| `nftables_logrotate_options.compress` | Compress rotated logs using gzip | `true` |
| `nftables_logrotate_options.nocreate` | Don't create new empty log file | `false` |
| `nftables_logrotate_options.dateext` | Add date extension to rotated logs | `true` |

### 3. Base Filter Chain Policies

| Variable | Description | Default |
|----------|-------------|---------|
| `nftables_input_default_policy` | Default policy for input chain (Options: 'accept', 'drop', 'reject') | `"drop"` |
| `nftables_forward_default_policy` | Default policy for forward chain (Options: 'accept', 'drop', 'reject') | `"drop"` |
| `nftables_output_default_policy` | Default policy for output chain (Options: 'accept', 'drop', 'reject') | `"drop"` |
| `nftables_log_input_dropped` | Enable/disable logging for dropped input packets | `true` |
| `nftables_log_forward_dropped` | Enable/disable logging for dropped forward packets | `true` |
| `nftables_log_output_dropped` | Enable/disable logging for dropped output packets | `true` |
| `nftables_log_input_dropped_rate_limit` | Rate limit for logging dropped input packets | `"10/minute"` |
| `nftables_log_input_dropped_burst` | Burst value for logging dropped input packets | `10` |
| `nftables_log_forward_dropped_rate_limit` | Rate limit for logging dropped forward packets | `"10/minute"` |
| `nftables_log_forward_dropped_burst` | Burst value for logging dropped forward packets | `10` |
| `nftables_log_output_dropped_rate_limit` | Rate limit for logging dropped output packets | `"10/minute"` |
| `nftables_log_output_dropped_burst` | Burst value for logging dropped output packets | `10` |

### 4. ICMP/Ping Settings

| Variable | Description | Default |
|----------|-------------|---------|
| `nftables_ping_input` | ICMP/Ping input configuration dictionary | See below |
| `nftables_ping_input.enabled` | Enable/disable ICMP/ping input | `true` |
| `nftables_ping_input.rate_limit` | Rate limit for ICMP/ping input | `"3/second"` |
| `nftables_ping_input.burst` | Burst value for ICMP/ping input | `4` |
| `nftables_ping_input.log` | Enable/disable logging for ICMP/ping input | `false` |
| `nftables_ping_input.comment` | Comment for ICMP/ping input rule | `"Allow limited ICMP/ping input"` |
| `nftables_ping_output` | ICMP/Ping output configuration dictionary | See below |
| `nftables_ping_output.enabled` | Enable/disable ICMP/ping output | `true` |
| `nftables_ping_output.rate_limit` | Rate limit for ICMP/ping output | `"6/second"` |
| `nftables_ping_output.burst` | Burst value for ICMP/ping output | `8` |
| `nftables_ping_output.log` | Enable/disable logging for ICMP/ping output | `false` |
| `nftables_ping_output.comment` | Comment for ICMP/ping output rule | `"Allow limited ICMP/ping output"` |

### 5. Basic Access Control Settings

| Variable | Description | Default |
|----------|-------------|---------|
| `nftables_blocked_reserved_ranges` | List of reserved address spaces to block (anti-spoofing protection) | See below |

**Reserved address ranges:**
By default, the following address ranges are blocked on external interfaces to prevent spoofing:
```yaml
nftables_blocked_reserved_ranges:
  - "0.0.0.0/8"        # "This" Network
  - "10.0.0.0/8"       # Private-Use Networks
  - "127.0.0.0/8"      # Loopback
  - "169.254.0.0/16"   # Link Local
  - "172.16.0.0/12"    # Private-Use Networks
  - "192.0.0.0/24"     # IETF Protocol Assignments
  - "192.0.2.0/24"     # Documentation (TEST-NET-1)
  - "224.0.0.0/3"      # Multicast & Reserved
```

To disable this protection or customize the ranges, modify this variable in your playbook.

### 6. Cluster Communication Settings

| Variable | Description | Default |
|----------|-------------|---------|
| `nftables_cluster_enabled` | Enable/disable cluster communication rules | `false` |
| `nftables_cluster_nodes` | List of IP addresses for cluster nodes | See defaults/main.yml |
| `nftables_cluster_rules` | Rules for communication between cluster nodes | See defaults/main.yml |

### 7. User-Defined Rules Settings

| Variable | Description | Default |
|----------|-------------|---------|
| `nftables_user_defined_input_enabled` | Enable/disable user-defined input rules | `false` |
| `nftables_user_defined_forward_enabled` | Enable/disable user-defined forward rules | `false` |
| `nftables_user_defined_output_enabled` | Enable/disable user-defined output rules | `false` |
| `nftables_user_defined_input_rules` | List of user-defined input rules | See defaults/main.yml |
| `nftables_user_defined_forward_rules` | List of user-defined forward rules | See defaults/main.yml |
| `nftables_user_defined_output_rules` | List of user-defined output rules | See defaults/main.yml |

**User-defined rule fields:**
- `source` (optional): Source IP/network (string)
- `destination` (optional): Destination IP/network (string)
- `protocol` (optional): Protocol (e.g. "tcp", "udp")
- `port` (optional): Single port (e.g. `22`), range (e.g. `1000-2000`), or comma-separated list (e.g. `22,80,443`) as a string
- `in_interface` (optional, forward only): Input interface (string)
- `out_interface` (optional, forward only): Output interface (string)
- `state` (optional): Connection state to match (e.g. "new", "established,related") - defaults to "new" if not specified
- `rate_limit` (optional): Rate limit in format "X/period" where period can be: second, minute, hour, day (e.g. "10/minute")
- `burst` (optional): Burst value for the rate limit (integer)
- `action`: Action to take (e.g. "accept", "drop")
- `log`: Enable/disable logging (boolean)
- `counter`: Enable/disable packet/byte counting for the rule (boolean)
- `comment`: Description of the rule (string)

**Example:**
```yaml
nftables_user_defined_output_rules:
  - source: "10.0.0.1"
    destination: "192.168.1.100"
    protocol: "tcp"
    port: "2221,2222"
    state: "new,established"
    rate_limit: "15/minute"
    burst: 8
    action: "accept"
    log: true
    counter: true
    comment: "Full example: output rule with all options"
```

### 8. NAT Rules Settings

| Variable | Description | Default |
|----------|-------------|---------|
| `nftables_nat_prerouting_enabled` | Enable/disable NAT prerouting rules | `false` |
| `nftables_nat_postrouting_enabled` | Enable/disable NAT postrouting rules | `false` |
| `nftables_nat_prerouting_rules` | List of DNAT (destination NAT) rules | See defaults/main.yml |
| `nftables_nat_postrouting_rules` | List of SNAT (source NAT) and masquerading rules | See defaults/main.yml |

**NAT rule fields:**
- `in_interface` (optional): Input interface (string)
- `out_interface` (optional): Output interface (string)
- `source` (optional): Source IP/network (string)
- `destination` (optional): Destination IP/network (string)
- `protocol` (optional): Protocol (e.g. "tcp", "udp")
- `port` (optional): Single port (e.g. `80`), range (e.g. `1000-2000`), or comma-separated list (e.g. `80,443`) as a string
- `nat_action`: NAT action ("dnat", "snat", "masquerade")
- `nat_to` (required for dnat/snat): Target address (e.g. `192.168.1.100:80` for dnat, `203.0.113.2` for snat)
- `counter`: Enable/disable packet/byte counting for the rule (boolean)
- `log`: Enable/disable logging (boolean)
- `comment`: Description of the rule (string)

**Examples:**
```yaml
nftables_nat_prerouting_rules:
  - in_interface: "eth0"
    protocol: "tcp"
    port: "80"
    nat_action: "dnat"
    nat_to: "192.168.1.100:80"
    counter: true
    log: false
    comment: "Forward HTTP to internal web server"
  - in_interface: "eth0"
    protocol: "tcp"
    port: "5000-5100"
    nat_action: "dnat"
    nat_to: "192.168.2.50"
    counter: true
    log: false
    comment: "Forward port range to DMZ server"

nftables_nat_postrouting_rules:
  - out_interface: "eth0"
    source: "192.168.1.0/24"
    nat_action: "masquerade"
    counter: true
    log: false
    comment: "NAT for LAN clients"
  - out_interface: "eth0"
    source: "192.168.2.0/24"
    nat_action: "snat"
    nat_to: "203.0.113.2"
    counter: true
    log: false
    comment: "SNAT for DMZ subnet"
```

## Tags

- `always` - Tasks that always run (variable loading and validation)
- `setup` - Setup tasks including OS-specific variables, requirements, and installation
- `init` - Initial setup tasks
- `validate` - Variable validation tasks
- `check` - Validation and verification tasks
- `requirements` - System requirements verification
- `reboot` - System reboot tasks (when required)
- `install` - Package installation tasks
- `configure` - Service configuration tasks
- `rules` - Firewall rules configuration
- `acl` - Access control list configuration
- `logrotate` - Log rotation configuration tasks
- `upgrade` - Package upgrade tasks (tagged with 'never' by default)

## Example Playbook

### Basic Firewall Setup
```yaml
---
- name: Configure NFTables Firewall
  hosts: all
  become: true
  roles:
    - role: grzegorzfranus.nftables
      vars:
        # Basic Configuration
        nftables_service_enabled: true
        nftables_configure_logrotate: true
        
        # Chain Policies
        nftables_input_default_policy: "drop"
        nftables_forward_default_policy: "drop"
        nftables_output_default_policy: "drop"
        
        # ICMP/Ping Settings
        nftables_ping_input:
          enabled: true
          rate_limit: "3/second"
          burst: 5
          log: true
          comment: "Allow controlled ICMP input"
```

### Advanced Configuration with NAT and User Rules
```yaml
---
- name: Configure NFTables with Advanced Features
  hosts: gateway_servers
  become: true
  roles:
    - role: grzegorzfranus.nftables
      vars:
        # Enable NAT for routing
        nftables_nat_prerouting_enabled: true
        nftables_nat_postrouting_enabled: true
        
        # Port forwarding rules
        nftables_nat_prerouting_rules:
          - in_interface: "eth0"
            protocol: "tcp"
            port: "80"
            nat_action: "dnat"
            nat_to: "192.168.1.100:80"
            log: false
            comment: "Forward HTTP to internal web server"
          - in_interface: "eth0"
            protocol: "tcp"
            port: "443"
            nat_action: "dnat"
            nat_to: "192.168.1.100:443"
            log: false
            comment: "Forward HTTPS to internal web server"
        
        # Masquerade internal network for internet access
        nftables_nat_postrouting_rules:
          - out_interface: "eth0"
            source: "192.168.1.0/24"
            nat_action: "masquerade"
            log: false
            comment: "NAT for LAN clients"
        
        # Enable user-defined rules
        nftables_user_defined_input_enabled: true
        nftables_user_defined_output_enabled: true
        
        # Custom input rules
        nftables_user_defined_input_rules:
          - protocol: "tcp"
            port: "80,443"
            state: "new,established"
            rate_limit: "30/minute"
            burst: 15
            action: "accept"
            log: false
            comment: "Allow HTTP and HTTPS traffic"
          - protocol: "udp"
            port: "53"
            state: "new"
            action: "accept"
            log: false
            comment: "Allow DNS queries"
        
        # Custom output rules
        nftables_user_defined_output_rules:
          - protocol: "udp"
            port: "53"
            state: "new"
            action: "accept"
            log: false
            comment: "Allow DNS resolution"
          - protocol: "tcp"
            port: "80,443"
            state: "established,related"
            action: "accept"
            log: false
            comment: "Allow HTTP and HTTPS traffic"
        
        # Customize blocked address ranges
        nftables_blocked_reserved_ranges:
          - "0.0.0.0/8"        # "This" Network
          - "127.0.0.0/8"      # Loopback
          - "169.254.0.0/16"   # Link Local
          - "192.0.0.0/24"     # IETF Protocol Assignments
          - "224.0.0.0/3"      # Multicast & Reserved
          # Note: 10.0.0.0/8 removed to allow local private network
```

### Cluster Configuration
```yaml
---
- name: Configure NFTables for Cluster
  hosts: cluster_nodes
  become: true
  roles:
    - role: grzegorzfranus.nftables
      vars:
        # Enable cluster communication
        nftables_cluster_enabled: true
        
        # Define cluster nodes
        nftables_cluster_nodes:
          - "192.168.10.10"
          - "192.168.10.11"
          - "192.168.10.12"
        
        # Define cluster communication rules
        nftables_cluster_rules:
          - port: 5432
            protocol: tcp
            log: true
            comment: "PostgreSQL cluster traffic"
          - port: 6379
            protocol: tcp
            log: true
            comment: "Redis replication"
          - port: 8301
            protocol: udp
            log: false
            comment: "Consul gossip protocol"
```

## License

Apache-2.0

## Author Information

This role was created by [Grzegorz Franus](https://github.com/grzegorzfranus).

## Contributing

Contributions, bug reports, and feature requests are welcome!

- Fork the repository and create your branch from `main`.
- Make your changes with clear, descriptive commit messages.
- Ensure your code passes all Molecule and lint tests.
- Submit a pull request describing your changes and the motivation.
- For major changes, please open an issue first to discuss what you would like to change.

If you have questions or suggestions, feel free to open an issue or contact the author via GitHub.