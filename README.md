# Vagrant GitLab Runner 🚀

Automated Ubuntu 22.04 VM setup with Docker and GitLab Runner for local CI/CD testing.

## Quick Start

```bash
# Clone and configure
git clone <repo-url>
cd vagrant-gitlab-runner
cp .env.example .env
# Edit .env with your GitLab registration token

# Provision VM
vagrant up
```

## Secrets

```bash
printf 'your-vault-password' > .vault_key.txt
ansible-vault create provisioning/secrets.yml --vault-password-file .vault_key.txt
```

Populate the vault with:

```yaml
gitlab_runner_registration_token: "glrt-..."
```

Update later with `ansible-vault edit provisioning/secrets.yml --vault-password-file .vault_key.txt`.

## System Components

- **Base**: Ubuntu 22.04 (2GB RAM, 2 vCPU)
- **Container Runtime**: Docker (via geerlingguy.docker 7.5.5)
- **CI Runner**: GitLab Runner (via riemers.gitlab-runner v2.0.12)
- **Executor**: Docker with Alpine image

## Configuration

- **VM Settings**: Edit `Vagrantfile`
- **Runner Config**: Edit `provisioning/playbook.yml`
- **Tokens**: Stored in encrypted `provisioning/secrets.yml`

## Commands

```bash
vagrant reload --provision    # Apply changes
vagrant destroy               # Remove VM
ansible-lint provisioning/   # Lint Ansible code
```

## CI/CD

Automated testing via GitHub Actions includes Ansible linting and Vagrantfile validation.

## License

MIT
