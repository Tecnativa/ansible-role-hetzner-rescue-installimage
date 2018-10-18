# Hetzner Rescue Installimage

[![GitHub license](https://img.shields.io/github/license/Tecnativa/ansible-role-hetzner-rescue-installimage.svg)](https://github.com/Tecnativa/ansible-role-hetzner-rescue-installimage/blob/master/LICENSE)
[![Ansible Galaxy](https://img.shields.io/badge/ansible--galaxy-tecnativa.hetzner_rescue_installimage-blue.svg)][galaxy]

Install your new Docker servers automatically in minutes

## Requirements

- This only works in Hetzner servers.
- The Hetzner server must be booted in rescue mode. This is the default for
  new servers as of today.

## Warnings

- Running this role will wipe all disks in the server.

## Role Variables

See default values and explanations in [`defaults/main.yml`][defaults].

## Example Playbook

This playbook should be usually separate from your main `site.yml` playbook,
as it would be used only to install new servers, and you don't want idempotence
nor running it anywhere else.

Let's call it `hetzner-install.yml`:

```yaml
- hosts: "{{ target }}"
  roles:
    - role: tecnativa.hetzner_rescue_installimage
      vars:
        # Disable SSH checking, it's mostly useless in this role's use case;
        # not done automatically because of the obvious insecurity
        ansible_ssh_extra_args:
          -o UserKnownHostsFile=/dev/null -o StrictHostKeyChecking=no
        # This is just an example, but declare any variables here
        swraid_level: 1
```

Now run it:

```bash
ansible-playbook netzner-install.yml -e target="$NEW_SERVER"
```

## Support

- [:octocat: GH project](https://github.com/Tecnativa/ansible-role-hetzner-rescue-installimage).
- [Install from Ansible Galaxy][galaxy].
- [Hetzner Installimage project](https://github.com/hetzneronline/installimage).
- [Hetzner rescue system instructions](https://wiki.hetzner.de/index.php/Hetzner_Rescue-System/en).

## License

Apache 2.

## Author Information

This project is maintained by:

[![Tecnativa logo](https://www.tecnativa.com/logo.png "Tecnativa")][Tecnativa]

[Tecnativa][] is an IT consulting company specialized in Odoo and provides Odoo
development, installation, maintenance and hosting services.

[defaults]: https://github.com/Tecnativa/ansible-role-hetzner-rescue-installimage/tree/master/defaults/main.yml
[galaxy]: https://galaxy.ansible.com/yajo/hetzner_rescue_installimage
[Tecnativa]: https://www.tecnativa.com
