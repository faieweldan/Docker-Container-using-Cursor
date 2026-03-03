# Docker MCP + Cursor (Postgres Playground)

This is a small “mess around” project where I tried running Docker containers using Cursor’s AI chat + a Docker MCP server (Model Context Protocol).

Instead of typing Docker commands the normal way, I set up Cursor so I can say things like “create a Postgres container” and it uses Docker MCP tools to do it.

## What I used
- Cursor (AI code editor / chat)
- Docker Desktop (to actually run containers)
- MCP (Model Context Protocol) + docker-mcp (lets Cursor talk to Docker)
- PostgreSQL (database container)
- Adminer (simple web UI for the database)
- Docker Compose (runs Postgres + Adminer together)

## What this project does
- Runs a Postgres container with:
  - DB name: RifDatabase
  - Username: admin
  - Password: ****
  - Port: 5432:5432
- Runs Adminer (web UI) on:
  - Port: 8081

## Folder structure
mcp-docker/
  docker-compose.yml

## How to run it (normal way)
If you just want to run it without MCP, from this folder:

docker compose up -d

Then open Adminer in your browser:
http://localhost:8081

Place login details

## How to stop / clean up
Stop containers:
docker compose down

Remove everything (containers + volumes):
docker compose down -v

## Notes
Main point of this repo is not the app itself — it’s the setup where Cursor can control Docker through MCP and natural language prompts.

If Docker MCP is working, Cursor should be able to:
- list containers
- create/start/stop containers
- view logs (example: Postgres startup logs)
- manage compose-based setups

A quick sandbox to understand MCP + Docker.
