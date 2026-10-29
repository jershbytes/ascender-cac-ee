# Ascender CAC Execution Environment

An Ansible execution environment for Ascender CAC, built on the AWX execution-environment image. It packages the collections and Python dependencies needed to run the project's Ansible automation.

## Included dependencies

- `ansible-homelab` collection from the `main` branch
- `ansible.posix`
- `community.general`
- `community.proxmox`
- Python package `proxmoxer`

See [requirements.yml](requirements.yml) and [requirements.txt](requirements.txt) for the dependency definitions.

## Build locally

Requirements: Python 3.10 or later, [uv](https://docs.astral.sh/uv/), and a container engine supported by Ansible Builder.

```sh
uv sync --locked
uv run ansible-builder build \
  --tag ascender-cac-ee:latest \
  --build-arg PYCMD=/usr/bin/python3.12
```

The execution-environment definition is in [execution-environment.yml](execution-environment.yml). Ansible Builder generates the `context/` build directory; it is excluded from version control.

## Published image

The Forgejo workflow builds and pushes the image to:

```text
git.jershlabs.xyz/jershbytes/ascender-cac-ee:<tag>
```

Pushes to `main` publish the `latest` tag. Version tags (`v*`) publish the matching version tag. Each workflow build is also tagged with its commit SHA. The workflow requires the `REGISTRY_USER` and `REGISTRY_TOKEN` repository secrets for registry authentication.

## License

This project is distributed under the MIT License. See [LICENSE](LICENSE).