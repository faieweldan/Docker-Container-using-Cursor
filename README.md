# Docker MCP + Cursor (Postgres Playground)

This is a small “mess around” project where I tried running Docker containers using Cursor’s AI chat + a Docker MCP server (Model Context Protocol).

Instead of typing Docker commands the normal way, I set up Cursor so I can say things like “create a Postgres container” and it uses Docker MCP tools to do it.

<img width="571" height="208" alt="image" src="https://github.com/user-attachments/assets/63d2607d-bc31-4214-b7a1-376ca1c7855b" />

---

## What I used
- Cursor (AI code editor / chat)
- Docker Desktop (to actually run containers)
- MCP (Model Context Protocol) + docker-mcp (lets Cursor talk to Docker)
- PostgreSQL (database container)
- Adminer (simple web UI for the database)
- Docker Compose (runs Postgres + Adminer together)

<img width="568" height="329" alt="image" src="https://github.com/user-attachments/assets/7acb72b9-6a84-40d4-ba77-0a3059e147ac" />

---

## What this project does
- Runs a Postgres container with:
  - DB name: RifDatabase
  - Username: admin
  - Password: ****
  - Port: 5432:5432
- Runs Adminer (web UI) on:
  - Port: 8081

---

## Folder structure
mcp-docker/
  docker-compose.yml

---

## MCP Setup (Important)

To allow Cursor to control Docker through natural language, I configured a Docker MCP server in Cursor.

This configuration lives **locally** on your machine (not inside this repo).

File location (Mac):
```
~/.cursor/mcp.json
```

Example configuration:

```json
{
  "mcpServers": {
    "docker": {
      "command": "uv",
      "args": [
        "run",
        "--with",
        "docker-mcp",
        "docker-mcp",
        "--access-mode=unrestricted"
      ],
      "env": {
        "DOCKER_HOST": "unix:///var/run/docker.sock",
        "UV_PYTHON": "/path/to/python3.13"
      }
    }
  }
}
```

Notes:
- `uv` is required to run the docker-mcp package.
- Python 3.12+ is required.
- `UV_PYTHON` ensures uv uses the correct Python version.
- Docker Desktop must be running.

After adding this file:
- Reload Cursor window
- Go to Settings → Tools & MCP
- Confirm docker shows green (connected)

Once connected, Cursor can:
- List containers
- Create containers
- Start/stop containers
- View logs
- Run Docker Compose setups

---

## How to run it (normal way)

If you just want to run it without MCP, from this folder:

```
docker compose up -d
```

Then open Adminer in your browser:
http://localhost:8081

<img width="625" height="479" alt="image" src="https://github.com/user-attachments/assets/3011d9a9-e533-419b-9218-633e82176f46" />
<img width="527" height="254" alt="Screenshot 2026-03-03 at 12 21 15 AM" src="https://github.com/user-attachments/assets/70b38f07-6ec9-47ab-ae64-208a2f4ad824" />
<img width="562" height="342" alt="image" src="https://github.com/user-attachments/assets/fd1dd275-dd9d-4a1b-a64c-dc0def1529d2" />

---

## How to stop / clean up

Stop containers:
```
docker compose down
```

Remove everything (containers + volumes):
```
docker compose down -v
```

---

## Notes

Main point of this repo is not the app itself — it’s the setup where Cursor can control Docker through MCP and natural language prompts.

If Docker MCP is working, Cursor should be able to:
- list containers
- create/start/stop containers
- view logs (example: Postgres startup logs)
- manage compose-based setups

A quick sandbox to understand MCP + Docker.
