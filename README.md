# Ansible Role: asciinema

Ansible role for installing [`asciinema`](https://asciinema.org/) terminal recorder into a Python3 VirtualEnv.

[![Build Status](https://www.travis-ci.org/PyratLabs/ansible-role-asciinema.svg?branch=master)](https://www.travis-ci.org/PyratLabs/ansible-role-asciinema)

## Requirements

This role has been tested on Ansible 2.7.0+ against the following Linux Distributions:

  - Amazon Linux 2
  - CentOS 8
  - CentOS 7
  - Debian 10
  - Fedora 29
  - Fedora 30
  - Fedora 31
  - Ubuntu 18.04 LTS

## Disclaimer

If you have any problems please create a GitHub issue, I maintain this role in
my spare time so I cannot promise a speedy fix delivery.

## Role Variables


| Variable                            | Description                                                                   | Default Value        |
|-------------------------------------|-------------------------------------------------------------------------------|----------------------|
| `asciinema_version`                 | Use a specific version of asciinema, eg. `2.0.2`. Specify `false` for latest. | `false`              |
| `asciinema_install_dir`             | Installation directory to put asciinema virtual environments.                 | `$HOME/.virtualenvs` |
| `asciinema_venv_name`               | Name for the asciinema Virtualenv.                                            | asciinema            |
| `asciinema_venv_suffix`             | Add a custom suffix to virtualenv.                                            | `asciinema_version`  |
| `asciinema_venv_site_packages`      | Allow venv to inherit packages from global site-packages.                     | `false`              |
| `asciinema_install_venv_helper`     | Install a venv helper to launch venv executables from a "bin" directory.      | `true`               |
| `asciinema_bin_dir`                 | "bin" directory to install venv-helpers to.                                   | `$HOME/bin`          |
| `asciinema_install_os_dependencies` | Allow role to install OS dependencies.                                        | `false`              |
| `asciinema_python3_path`            | Specify a path to a specific python version to use in virtualenv.             | _NULL_               |

## Dependencies

No dependencies on other roles.

## Example Playbook

Example playbook for installing to single user:

```yaml
- hosts: asciinema_hosts
  roles:
     - { role: xanmanning.asciinema, asciinema_version: 2.0.2 }
```

Example playbook for installing the latest asciinema version globally:

```yaml
---
- hosts: asciinema_hosts
  become: true
  vars:
    asciinema_install_os_dependencies: true
    asciinema_install_dir: /opt/asciinema/bin
    asciinema_bin_dir: /usr/bin
    asciinema_venv_ame: current
  roles:
    - role: xanmanning.asciinema
```

### Activating the asciinema venv

You need to activate the python3 virtual environment to be able to access `asciinema`.
This is done as per the below:

```bash
source {{ asciinema_install_dir }}/{{ asciinema_venv_name }}/bin/activate
```

In the above example global installation playbook, this would look like the
following:

```bash
source /opt/asciinema/bin/current/bin/activate
```

## License

[BSD 3-clause](LICENSE.txt)

## Author Information

[Xan Manning](https://xanmanning.co.uk/)
