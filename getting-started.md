# Getting Started

Deploy your first AI agent in under five minutes.

---

## 1. Install

```bash
pip install cognos
```

Requires Python 3.10+.

---

## 2. Login

```bash
cognos login
```

Opens a browser for OAuth authentication. Your token is saved to `~/.cognos/credentials`.

---

## 3. Write your agent

Create a file called `agent.py`:

```python
from cognos import Agent

agent = Agent(
    name="my-agent",
    model="gpt-4o",
    memory=True,
    tools=["web"]
)

agent.deploy()
```

---

## 4. Deploy

```bash
cognos deploy
```

Output:

```
  Deploying  my-agent

  ✓  Packaging agent...
  ✓  Uploading to Cognos Cloud...
  ✓  Provisioning runtime...
  ✓  Allocating memory store...
  ✓  Registering tools: web...
  ✓  Starting container...
  ✓  Health check passed...

  ● Agent deployed successfully

  Dashboard  https://cloud.cognos.ai/agents/my-agent
  API        POST https://api.cognos.ai/v1/agents/my-agent/run
  Status     Running
```

---

## What you get

Every deployed agent automatically gets:

| Feature | Description |
|---|---|
| **Live dashboard** | Logs, metrics, cost, memory — at `cloud.cognos.ai/agents/{name}` |
| **REST API endpoint** | `POST https://api.cognos.ai/v1/agents/{name}/run` |
| **Auto-restart** | Cognos restarts the agent if it crashes |
| **Persistent memory** | Context stored across sessions (when `memory=True`) |
| **Cron scheduling** | Run on any schedule (when `cron` is set) |
| **Webhook triggers** | Trigger via HTTP from any external service |

---

## Next steps

- [SDK Reference](./sdk.md) — full Agent API
- [CLI Reference](./cli.md) — all commands
- [Examples](../examples/) — three ready-to-deploy agents
