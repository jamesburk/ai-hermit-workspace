# Tool Notes

## exec (shell)

WSL2 Ubuntu on Polaris. Useful commands:

### Local Operations
- ollama list / ollama ps -- installed and running models
- nvidia-smi -- GPU temp and VRAM usage
- openclaw status -- gateway health
- openclaw gateway restart -- restart after config changes
- docker ps | grep openclaw -- container status

### Dev Tools
- git, node, pnpm, bun -- available in WSL2
- docker compose -- from /home/jburk/Projects/ai-hermit/openclaw/

### Scripts
- ~/.openclaw/scripts/memory-audit.sh [--verbose] -- full system report
- ~/.openclaw/scripts/validate-config.mjs -- validate openclaw.json

### Remote Operations (requires Tailscale)
- tailscale status -- mesh network state
- tailscale ping aurora -- check Aurora R9 reachability
- curl http://aurora:18789/api/health -- Aurora gateway health (when connected)

## memory_search / memory_get

- memory_search(query) -- keyword search across all memory files and MEMORY.md
- memory_get(path) -- read a specific file, e.g. memory/2026-02-24-setup.md

## browser

Web fetch and page analysis. Use for checking docs, researching solutions, or verifying services.

## Conventions

- Match codebase style and conventions when producing code
- For multi-step tasks, outline the plan before executing
- If a tool call fails, diagnose before retrying -- don't brute force
- Prefer reading code before modifying -- understand context first
