# Changelog

All notable changes to ansible-role-do_network_routing are documented here. The format is based on
[Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and this project adheres to
[Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [1.0.0] - 2025-02-18

### Added
- Initial release of the `do_network_routing` Ansible role, published on Ansible Galaxy.
- Retrieves the gateway's public IP from the DigitalOcean metadata endpoint (`169.254.169.254`).
- Adds a route to the metadata endpoint via the gateway's public IP (idempotent — skipped if the route already exists).
- Changes the system default gateway to a specified private IP (`gateway_private_ip`).
- Rewrites Netplan configuration (`/etc/netplan/50-cloud-init.yaml`) to remove the default route from the public interface (`eth0`) and add it to the internal interface (`eth1`).
- Applies the Netplan changes.

[Unreleased]: https://github.com/brett-buskirk/ansible-role-do_network_routing/compare/v1.0.0...HEAD
[1.0.0]: https://github.com/brett-buskirk/ansible-role-do_network_routing/releases/tag/v1.0.0
