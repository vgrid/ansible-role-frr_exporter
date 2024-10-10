# Ansible Role: FRR exporter

[![CI](https://github.com/vgrid/ansible-role-frr_exporter/workflows/CI/badge.svg?event=push)](https://github.com/vgrid/ansible-role-frr_exporter/actions?query=workflow%3ACI)

This role installs Prometheus' [FRR Exporter](https://github.com/tynany/frr_exporter) on Linux hosts, and configures a systemd unit file so the service can run and be controlled by systemd.

## Credit

This role is a modified version of the ansible-role-node exporter by by [Jeff Geerling](https://www.jeffgeerling.com/), author of [Ansible for DevOps](https://www.ansiblefordevops.com/). Thanks to Jeff it was very quick to get this up and running.

## Requirements

N/A

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    frr_exporter_version: '1.1.3'

The version of FRR Exporter to install. Available releases can be found on the [tags](https://github.com/tynany/frr_exporter/tags) listing in the FRR Exporter repository. Drop the `v` off the tag.

If you change the version, the `frr_exporter` binary will be replaced with the updated version, and the service will be restarted.

    frr_exporter_arch: 'amd64'
    frr_exporter_download_url: https://github.com/tynany/frr_exporter/releases/download/v{{ frr_exporter_version }}/frr_exporter-{{ frr_exporter_version }}.linux-{{ frr_exporter_arch }}.tar.gz

The architecture and download URL for FRR Exporter. If you're on a Raspberry Pi running Raspbian, you may need to override the `arch` value with `armv7`.

    frr_exporter_bin_path: /usr/local/bin/frr_exporter

The path where the `frr_exporter` binary will be installed.

    frr_exporter_host: 'localhost'
    frr_exporter_port: 9100

Host and port on which FRR Exporter will listen.

    frr_exporter_options: ''

Any additional options to pass to `frr_exporter` when it starts, e.g. `--no-collector.bgp` if you want to ignore BGP collection

    frr_exporter_state: started
    frr_exporter_enabled: true

Controls for the `frr_exporter` service.

## Dependencies

None.

## Example Playbook

    - hosts: all
      roles:
        - role: vgrid.frr_exporter

## License

MIT / BSD

