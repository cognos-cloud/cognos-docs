# Runtime

The Cognos Cloud Runtime keeps your agent running continuously in a managed container.

## What it handles

| Feature | Description |
|---|---|
| **Continuous execution** | Agent runs forever in an isolated container |
| **Auto-restart** | Restarted automatically on crash or OOM |
| **Cron scheduling** | Triggered on any cron expression |
| **Webhook triggers** | Triggered via HTTP from any service |
| **Live REST API** | `POST /agents/{name}/run` is live on deploy |
| **Health checks** | Container health monitored continuously |
| **Log streaming** | All stdout/stderr sent to dashboard |
| **Horizontal scaling** | Coming Soon |

## Cron expressions

```python
agent = Agent(
    name="my-agent",
    cron="0 9 * * *",      # every day at 9am UTC
)
```

Common expressions:

| Expression | Schedule |
|---|---|
| `0 9 * * *` | Every day at 9am |
| `0 9 * * 1` | Every Monday at 9am |
| `*/15 * * * *` | Every 15 minutes |
| `0 0 1 * *` | First of every month |
| `0 9-17 * * 1-5` | Every hour 9am–5pm, weekdays |

## Webhook triggers

```python
agent = Agent(
    name="github-agent",
    endpoint="/webhook/github",
)
```

After deploy, your agent listens at:
```
POST https://api.cognos.ai/v1/agents/github-agent/webhook/github
```

## Restart policy

Cognos restarts your agent automatically if:
- The process exits unexpectedly
- The health check endpoint stops responding
- The container runs out of memory

You'll see each restart in the dashboard logs with the reason.

## Resource limits

| Tier | Memory | CPU | Timeout |
|---|---|---|---|
| Starter | 512 MB | 0.5 vCPU | 60s per run |
| Pro | 2 GB | 2 vCPU | 300s per run |
| Enterprise | Custom | Custom | Custom |
