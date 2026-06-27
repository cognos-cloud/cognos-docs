# SDK Reference

## Installation

```bash
pip install cognos
```

---

## Agent

The core primitive. Defines an agent and its deployment configuration.

```python
from cognos import Agent

agent = Agent(
    name: str,              # Unique identifier. Used in dashboard URL + API path.
    model: str,             # LLM model. Default: "gpt-4o"
    memory: bool,           # Enable persistent memory. Default: False
    tools: list[str],       # Tool names or @tool-decorated functions.
    cron: str | None,       # Cron expression. e.g. "0 9 * * *"
    endpoint: str | None,   # Webhook path. e.g. "/webhook/github"
    instructions: str,      # System prompt / agent persona.
    policy: Policy | None,  # Governance config. See Policy.
)
```

### Methods

| Method | Description |
|---|---|
| `agent.deploy()` | Package and deploy to Cognos Cloud |
| `agent.start()` | Start a stopped agent |
| `agent.stop()` | Stop a running agent |
| `agent.restart()` | Restart the container |
| `agent.logs(tail, follow)` | Stream logs |
| `agent.delete()` | Delete agent and all resources |

---

## Supported models

| Provider | Models |
|---|---|
| OpenAI | `gpt-4o`, `gpt-4o-mini`, `o1`, `o3-mini` |
| Anthropic | `claude-3-5-sonnet-20241022`, `claude-3-haiku-20240307` |
| Google | `gemini-2.0-flash`, `gemini-1.5-pro` |
| Local (Ollama) | `ollama://llama3.2`, `ollama://mistral`, `ollama://qwen2.5` |

---

## @tool decorator

Register any Python function as a tool:

```python
from cognos import tool

@tool(name="get-sol-price", description="Returns current SOL price in USD")
def get_sol_price() -> str:
    import requests
    data = requests.get("https://api.coingecko.com/api/v3/simple/price?ids=solana&vs_currencies=usd").json()
    return str(data["solana"]["usd"])

agent = Agent(
    name="price-agent",
    tools=[get_sol_price],
)
```

Parameters must be typed. Supported types: `str`, `int`, `float`, `bool`.
Return type must be `str`.

---

## Memory

Enabled with `memory=True`. No further config required.

For direct access:

```python
from cognos.memory import Memory

mem = Memory(agent_name="my-agent")
mem.write("session-123", "User prefers Python and dark mode")
results = mem.search("user preferences", top_k=3)
```

---

## Policy

```python
from cognos import Policy

policy = Policy(
    max_spend_per_day=5.00,
    max_spend_per_run=0.50,
    require_human_approval=["send_payment"],
    allowed_tools=["slack", "notion"],
    max_runs_per_hour=10,
)

agent = Agent(name="my-agent", policy=policy)
```

---

## Environment variables

| Variable | Description |
|---|---|
| `COGNOS_API_KEY` | API key (alternative to `cognos login`) |
| `COGNOS_API_URL` | Override API base URL (for self-hosted) |
| `OPENAI_API_KEY` | Required for OpenAI models |
| `ANTHROPIC_API_KEY` | Required for Anthropic models |
| `GOOGLE_API_KEY` | Required for Google models |
