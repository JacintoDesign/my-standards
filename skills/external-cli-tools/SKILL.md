---
name: external-cli-tools
description: Use when you already know the operation you need and a CLI tool can perform it directly — prefer CLI over MCP when the operation is straightforward and the command is known, to avoid MCP round-trips. Covers Vercel CLI and other installed tools.
---

# External CLI Tools

## Overview

Reference for CLI tools available in this environment and when to prefer them over their MCP equivalents. Use CLI directly when the operation is known — it's faster and avoids MCP overhead.

## CLI vs MCP Decision Rule

| Situation | Use |
|-----------|-----|
| You know exactly what you need | CLI |
| You need to explore, search, or discover | MCP |
| Bulk/multi-step operations | MCP (better error handling) |
| One-shot read or status check | CLI |

---

## Vercel CLI

**Install check:** `vercel --version`

### When to Use CLI Instead of Vercel MCP

Use the Vercel CLI in any session where you already know the operation — deployment status, project listing, or environment variable inspection. Fall back to Vercel MCP for discovery, complex filtering, or operations that need structured responses.

### Command Reference

| Goal | Command |
|------|---------|
| List recent deployments | `vercel ls` |
| List deployments for a specific project | `vercel ls <project-name>` |
| Show deployment details | `vercel inspect <deployment-url>` |
| List all projects | `vercel projects ls` |
| List environment variables | `vercel env ls` |
| Pull env vars to local `.env` | `vercel env pull` |
| Add an environment variable | `vercel env add <name> <environment>` |
| Remove an environment variable | `vercel env rm <name> <environment>` |
| Link current directory to a project | `vercel link` |
| View build/runtime logs | `vercel logs <deployment-url>` |

### Environment Targets

Vercel has three targets: `production`, `preview`, `development`. Most `env` commands accept a target as the last argument.

---

<!-- Add new CLI sections below this line as tools are installed -->
