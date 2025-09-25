# CRUSH.md

## Project Overview
Vagrant + Ansible setup for provisioning Ubuntu 22.04 VM with Docker and GitLab Runner for CI/CD pipelines using Docker executors.

## Prerequisites
- Vagrant 2.x
- Ansible 2.12+
- VirtualBox provider
- GITLAB_TOKEN env var for runner registration (set in .env or environment)

## Commands

### Setup and Provisioning
- `vagrant up` -- Start VM and run provisioning.
- `vagrant destroy` -- Teardown VM and cleanup.
- `vagrant ssh` -- Access the running VM.
- `ansible-playbook provisioning/playbook.yml --extra-vars "gitlab_runner_registration_token=$GITLAB_TOKEN"` -- Manual provisioning.

### Linting
- `ansible-lint provisioning/` -- Lint Ansible playbooks, roles, and tasks for best practices.
- `yamllint provisioning/` -- Validate YAML syntax in all provisioning files.
- `ansible-lint provisioning/playbook.yml` -- Lint a single file.

### Testing
- `ansible-playbook --check provisioning/playbook.yml` -- Dry-run full provisioning (idempotency check).
- `ansible-playbook --check provisioning/playbook.yml --tags docker` -- Test single task/tag (e.g., docker or gitlab-runner).
- `molecule test` -- If Molecule is set up for role testing (not present; suggest adding for roles/).

### Development
- No build step; this is Infrastructure as Code (IaC).
- Reload changes: `vagrant reload --provision`.

## Code Style Guidelines

### YAML (Ansible Playbooks/Tasks)
- Indentation: 2 spaces; no tabs.
- Task names: Descriptive, imperative (e.g., "Install Docker via APT").
- Keys: snake_case (e.g., ansible_python_interpreter).
- Strings: Quote only if containing special chars; prefer unquoted for booleans/lists.
- Tags: Always add tags to tasks (e.g., tags: [docker]).
- Handlers: Use for notifications; idempotent.
- Variables: Use extra_vars for env-specific (e.g., tokens); defaults in roles/.
- Error handling: Use `become: true` for sudo; `failed_when` for custom failures; retries with `until`.

### Ruby (Vagrantfile)
- Syntax: Standard Ruby 2.x+.
- Naming: snake_case for methods/vars (e.g., config.vm.box).
- Blocks: Use do/end for multi-line configs.
- Comments: Minimal; explain non-obvious (none added unless requested).

### General Conventions
- File naming: kebab-case (e.g., docker.yml).
- Imports/Includes: Use include_tasks for modularity.
- Types: YAML implicit (string/number/boolean).
- Secrets: Never hardcode; use env vars or vault (e.g., GITLAB_TOKEN).
- Formatting: Run yamllint/ansible-lint before commits.
- Git: Ignore .vagrant/, .env; commit idempotent configs.

## Notes
- Project structure: Vagrantfile roots config; provisioning/ holds Ansible (playbook.yml includes tasks/docker.yml, tasks/gitlab-runner.yml).
- VM specs: 2GB RAM, 2 CPUs (editable in Vagrantfile).
- Extend: Add roles/ for reusable components; use Molecule for testing."
<parameter name="file_path">/home/jonas/Documents/vagrant/CRUSH.md