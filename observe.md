# Observe

**Status: Coming Soon** — live logs and basic metrics are available now. Full trace explorer is in development.

---

Every agent execution is recorded as a structured trace. View them in the dashboard at `cloud.cognos.ai/agents/{name}`.

## What's available now

| Feature | Status |
|---|---|
| Live execution logs | ✅ Live |
| CPU usage + sparkline | ✅ Live |
| Latency metrics | ✅ Live |
| Per-run cost tracking | ✅ Live |
| Request count / failure rate | ✅ Live |
| Full tool call traces | 🔵 Coming Soon |
| Execution timeline | 🔵 Coming Soon |
| Alerting on failure / latency | 🔵 Coming Soon |

## Reading logs

```bash
# Last 100 lines
cognos logs my-agent

# Stream continuously
cognos logs my-agent --follow

# Last 50 lines
cognos logs my-agent --tail 50
```

## Example trace

```
0ms    Cron triggered (0 9 * * *)
12ms   Memory: loaded 8 items from context store
240ms  → web.search("top AI news last 24h")
910ms  ← web: 14 results (670ms)
1.2s   → web.search("tech funding news today")
1.8s   ← web: 9 results (580ms)
3.1s   → slack.post(channel="#research")
3.4s   ← slack: message sent
3.5s   ● Complete · 3.5s · $0.04
```

## Cost tracking

Every run reports:
- `cost_usd` — total LLM cost for this execution
- `latency_ms` — wall-clock time from trigger to completion
- `memory_writes` — items written to the memory store

Costs are shown per-run, per-day, and in total on the dashboard.
