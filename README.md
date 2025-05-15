# Strfry Indexer Relay

Ansible playbook to deploy a [strfry](https://github.com/hoytech/strfry) nostr relay.

## Prerequisites

- Python 3.10+
- [uv](https://github.com/astral/uv) package manager
- Debian/Ubuntu target system

## Setup

1. Install uv:
```sh
curl -LsSf https://astral.sh/uv/install.sh | sh
```

2. Install dependencies:
```sh
uv install
```

3. Create a virtual environment:
```sh
uv venv
```

## Configuration

1. Fill in your server details in `inventory/hosts.yml`
2. Customize the deployment in `roles/strfry/defaults/main.yml`
3. Set your relay's domain name in `roles/nginx/defaults/main.yml`

## Deploy

Run the playbook:
```sh
uv run ansible-playbook -i inventory/hosts.yml site.yml
```

This will:
1. Install system dependencies
2. Create strfry user and directories
3. Clone and build strfry from source
4. Configure and start systemd service

## Verify

Check service status:
```sh
ssh your-server "systemctl status strfry"
```

Test the relay:
```sh
curl http://your-server:7777
```
