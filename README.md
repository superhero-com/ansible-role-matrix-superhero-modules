# Superhero custom matrix modules Ansible role

This is an [Ansible](https://www.ansible.com/) role which installs custom matrix python modules from specific github repo.

This role is intended for use with [`spantaleev/matrix-docker-ansible-deploy` book](https://github.com/spantaleev/matrix-docker-ansible-deploy).


# Install
This role might fail for initial matrix server installation, do not include on first time setup, after it is finished rerun with the role included

Add in `requirements.yml`

```yaml
- src: git+https://github.com/superhero-com/ansible-role-matrix-superhero-modules.git
  version: v1.0.0-0
  name: matrix_superhero_modules
```

Then run `just roles`

Add in `setup.yml`

```yaml
- role: galaxy/matrix_superhero_modules
```

## Usage

Example config (vars.yml):

```yaml
matrix_superhero_modules_enabled: true # default is false
matrix_superhero_modules_token: "ghp_.." #github personal token to access private repos
matrix_superhero_modules_git_repo: "https://x-access-token:{{ matrix_superhero_modules_token }}@github.com/***org***/***repo***.git"
matrix_superhero_modules_git_path: "/matrix/synapse-patch" # path on the matrix host to clone the files before mapping to the container
matrix_superhero_modules_git_src_path: "/custom_modules" # relative path in the cloned repo files where the .py files reside
matrix_superhero_modules_version: "main" # git branch/version
# configure account validation module
matrix_superhero_modules_trigger_account_validation_enabled: true
matrix_superhero_modules_trigger_account_validation_config:
  backend_base_url: "https://{{ matrix_server_fqn_matrix }}/callback"
# configure room name checker module
matrix_superhero_modules_room_name_checker_enabled: true
matrix_superhero_modules_room_name_checker_config:
  admin_users:
  - "@admin:{{ matrix_domain }}"
  - "@backendbot:{{ matrix_domain }}"
```