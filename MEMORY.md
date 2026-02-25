# Memory -- Hermit

## System Status (updated 2026-02-24)

- **Ollama:** v0.15.6 running, localhost:11434
- **OpenClaw:** v2026.2.20, gateway port 18789, Docker container
- **Tailscale:** not installed yet (planned for cross-machine connectivity)
- **Primary model:** qwen3:8b (5.2GB, installed) -- general-purpose chat + reasoning
- **Code model:** qwen2.5-coder:7b (4.7GB, installed) -- coding tasks
- **Heartbeat model:** gpt-oss:20b (13GB, installed)
- **Cloud fallback:** anthropic/claude-opus-4-6 (configured via auth profile)
- **GPU:** RTX 5070 Laptop, 8151 MiB VRAM
- **Disk:** 904GB free (6% used)
- **Channels:** Signal configured (not registered), Matrix configured

## Infrastructure

- **Aurora R9:** Not yet connected (Tailscale pending on both machines)
- **Aurora gateway:** Will be reachable at http://aurora:18789 via Tailscale
- **Matrix homeserver:** matrix.northbend.net

## Pending Actions

1. Install Tailscale on Polaris for cross-machine connectivity
2. Signal onboarding: openclaw onboard --channel signal (number: +12066017143)
3. Matrix onboarding: verify hermit bot access to matrix.northbend.net
4. Register Windows startup task: scripts/register-startup-task.ps1

## Key Decisions

- 2026-02-24: qwen3:8b as primary general model (fits 8GB VRAM with room for heartbeat)
- 2026-02-24: qwen2.5-coder:7b for coding contexts (faster, code-tuned)
- 2026-02-24: gpt-oss:20b for heartbeat checks (lightweight, keeps coding models free)
- 2026-02-24: anthropic/claude-opus-4-6 as cloud fallback
- 2026-02-24: Workspace architecture aligned with Aurora reference

## Incidents

- 2026-02-07: Initial workspace setup and bootstrap completed
- 2026-02-08: GitHub sync configured (auto-push on commit)

## Reference

- OpenClaw docs: https://docs.openclaw.ai/
- Gateway UI: http://localhost:18789
- Project repo: /home/jburk/Projects/ai-hermit/
- Code patterns: memory/code-patterns.md
