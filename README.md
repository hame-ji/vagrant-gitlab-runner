# Vagrant GitLab Runner Setup 🚀

## Overview
This project provisions a Ubuntu 22.04 VM using Vagrant and Ansible, installing Docker and a GitLab Runner configured for Docker executors. Ideal for local CI/CD testing.

## Prerequisites 📋
- Vagrant 2.x
- Ansible 2.12+
- VirtualBox
- `GITLAB_TOKEN` environment variable for runner registration

## Quick Start
1. Clone the repository.
2. Set `export GITLAB_TOKEN=your_token`.
3. Run `vagrant up` to provision the VM.
4. Access the VM with `vagrant ssh`.
5. Verify runner registration in your GitLab project.

## Usage ⚙️
- Reload changes: `vagrant reload --provision`
- Destroy VM: `vagrant destroy`
- Manual provisioning: `ansible-playbook provisioning/playbook.yml --extra-vars "gitlab_runner_registration_token=$GITLAB_TOKEN"`

## Configuration
Edit `Vagrantfile` for VM specs or `provisioning/playbook.yml` for Ansible tasks. Secrets are handled via environment variables.

## Testing and Linting 🧪
- Lint: `ansible-lint provisioning/`
- Dry-run: `ansible-playbook --check provisioning/playbook.yml`

## License
MIT