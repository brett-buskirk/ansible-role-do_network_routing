# ansible-role-do_network_routing

This Ansible role configures network routing on [DigitalOcean](https://m.do.co/c/b2ef32b53bbc) (DO) droplets running Ubuntu systems, including setting the default gateway and adding a route for a DO metadata endpoint.

## Requirements

* An Ubuntu-based system
* Ansible 2.9 or later
* Root privileges (via `become: true`)
* A droplet hosted on DigitalOcean

## Role Variables

| Variable Name | Description | Default Value |
|---|---|---|
| `gateway_private_ip` | The private IP address of the gateway to be set as the default route. | None (required) |

## Dependencies

This role has no dependencies.

## Example Playbook

```yaml
- hosts: your_hosts
  become: true
  vars:
    gateway_private_ip: 192.168.1.1  # Replace with your gateway's private IP
  roles:
    - brett-buskirk.do_network_routing
```

## Installation

You can install this role using Ansible Galaxy:

```shell
ansible-galaxy role install brett-buskirk.do_network_routing
```

Or you can include it in your requirements.yml file:

```yaml
---
  - name: brett-buskirk.do_network_routing
```

Then install it using:

```shell
ansible-galaxy install -r requirements.yml
```

## Role Tasks

This role performs the following tasks:

* **Retrieve Gateway's Public IP:** Obtains the gateway's public IP address from the metadata server at `http://169.254.169.254`.
* **Check for Existing Route:** Checks if a route to the metadata endpoint (`169.254.169.254`) already exists.
* **Add Route to Metadata Endpoint:** Adds a route to the metadata endpoint via the gateway's public IP if it doesn't already exist.
* **Change Default Gateway:** Changes the system's default gateway to the specified private IP address (`gateway_private_ip`).
* **Modify Netplan Configuration:** Updates the Netplan configuration (`/etc/netplan/50-cloud-init.yaml`) to:
  * Remove the default route from the public interface (`eth0`).
  * Add a route to the internal interface (`eth1`) via the specified private gateway IP.
* **Apply Netplan Changes:** Applies the Netplan configuration with debug output enabled.

## Usage

* **Define gateway_private_ip:** In your playbook, set the `gateway_private_ip` variable to the private IP address of your gateway.
* **Include the role:** Add the `do_network_routing` role to your playbook.

This role will then configure the routing as described in the [Role Tasks](#role-tasks) section.

## License

MIT

## Author Information

Brett Buskirk

## Galaxy Tags

```shell
networking, routing, gateway, netplan, metadata, cloud, system, configuration
```
