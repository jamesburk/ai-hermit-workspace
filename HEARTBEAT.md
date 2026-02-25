# Heartbeat Tasks

Run these checks in order. Keep it fast -- one exec call per check. Only produce output if something needs attention.

## Checks

1. Ollama: exec ollama ps -- verify responding. Flag if exit code != 0.
2. Gateway: exec openclaw status -- verify running. Flag if not running.
3. GPU: exec nvidia-smi --query-gpu=temperature.gpu,memory.used --format=csv,noheader -- flag if temp > 85C or VRAM > 7500 MiB.
4. Disk: exec df -h /home | tail -1 -- flag if usage > 90%.
5. Tailscale: exec tailscale ping aurora --timeout 3s -- flag if unreachable (warn only, do not fail heartbeat).

## On failure

Write a timestamped entry to memory/heartbeat-alerts.md with the error details.

## State

After checks, update heartbeat-state.json in this workspace with current timestamps and results.

## If everything is OK

Reply HEARTBEAT_OK. Do not produce any other output.
