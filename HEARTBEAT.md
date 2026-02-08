# Hermit — Heartbeat Checklist

> This file is executed on scheduled heartbeat intervals.
> Keep tasks lightweight — heartbeats should complete quickly.

## On Each Heartbeat

- [ ] Check for any pending reminders or scheduled tasks in today's daily log
- [ ] Review recent memory entries for anything that needs follow-up
- [ ] Verify gateway is responsive (if health-check tools are available)

## Notes

- Heartbeat runs are non-interactive — produce output only when there is something actionable.
- If nothing needs attention, respond with `NO_REPLY`.
