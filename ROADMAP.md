# Roadmap

This is a small, single-purpose Ansible role that configures network routing on DigitalOcean
droplets. It is feature-complete for its intended job and shipped as `v1.0.0` on Ansible Galaxy.

## Maintenance

The role is in maintenance mode: it will be updated as needed to track DigitalOcean's droplet
networking and to stay compatible with current Ubuntu / Netplan releases. Bug reports and
compatibility fixes are welcome.

## Possible future improvements

- [ ] Make interface names configurable (`public_interface` / `private_interface`) instead of hard-coding `eth0` / `eth1`, for droplets whose interfaces are named differently.
- [ ] Add idempotency guards to the Netplan edits so re-runs are cleanly no-ops, and add Molecule-based test coverage.
