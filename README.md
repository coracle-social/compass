# Strfry Indexer Relay

Ansible playbook to deploy a [strfry](https://github.com/hoytech/strfry) nostr relay tailored to indexing kind 10002.

NOTE: please do not deploy this unless you expect to be serving a significant number of requests (for example, if you run a popular client). The nostr network only needs a few indexers to be available; any more only add unnecessary load on any mirrors that are configured.

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
4. Start a strfry relay that only accepts kind 10002
5. Start a strfry router that replicates kind 10002 events to/from selected relays
6. Set up a nginx reverse proxy with a SSL certificate for your domain
