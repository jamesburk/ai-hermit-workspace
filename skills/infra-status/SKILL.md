# Skill -- Infrastructure Status

Comprehensive health check across local and remote systems.

## Commands

- `/status` -- Full infrastructure check (local + remote)
- `/status local` -- Local checks only (Polaris)
- `/status aurora` -- Remote Aurora R9 checks only (requires Tailscale)

## Checks

### Local (Polaris)

```bash
echo "=== Polaris Local Status ==="

echo "-- Ollama --"
ollama ps 2>&1

echo "-- GPU --"
nvidia-smi --query-gpu=name,temperature.gpu,memory.used,memory.total,utilization.gpu --format=csv,noheader 2>&1

echo "-- Gateway --"
docker ps --filter "name=openclaw" --format "{{.Names}}\t{{.Status}}" 2>&1

echo "-- Disk --"
df -h /home | tail -1 2>&1

echo "-- Docker --"
docker ps --format "{{.Names}}\t{{.Status}}" 2>&1
```

### Remote (Aurora R9 -- requires Tailscale)

```bash
echo "=== Aurora R9 Status ==="

echo "-- Tailscale --"
tailscale ping aurora --timeout 3s 2>&1

echo "-- Gateway Health --"
curl -s --connect-timeout 5 http://aurora:18789/api/health 2>&1 || echo "unreachable"

echo "-- Ollama --"
curl -s --connect-timeout 5 http://aurora:11434/api/tags 2>&1 | head -20 || echo "unreachable"
```

### Services

```bash
echo "=== External Services ==="

echo "-- Matrix --"
curl -s --connect-timeout 5 https://matrix.northbend.net/_matrix/federation/v1/version 2>&1 || echo "unreachable"
```

## Output Format

Present results as a status table:

```
Service          Status    Details
-----------      ------    -------
Ollama           OK        qwen3:8b loaded, 3.2GB VRAM
GPU              OK        42C, 3200/8151 MiB
Gateway          OK        Up 4 days
Disk             OK        6% used (904GB free)
Aurora           WARN      Tailscale not installed
Matrix           OK        v1.x.x responding
```

## Behavior

- Gracefully handle offline/unreachable systems (show WARN, don't fail)
- If Tailscale is not installed, skip remote checks with a note
- Cache results in memory/infra-status-cache.md for offline reference
- Flag anything that needs attention (high temp, low disk, service down)
