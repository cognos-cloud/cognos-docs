# Memory

**Status: Coming Soon** — basic read/write is available now. Vector search and per-user namespaces are in development.

---

Cognos Cloud Memory gives agents persistent intelligence across sessions. Set `memory=True` and your agent automatically reads prior context on startup and writes new items after each run.

## Basic usage

```python
agent = Agent(
    name="support-agent",
    memory=True,   # that's it
)
```

Every run, the agent:
1. Reads relevant items from the memory store
2. Includes them in the LLM context
3. Writes new items after the run completes

## What's available now

| Feature | Status |
|---|---|
| Conversation history | ✅ Live |
| Long-term context store | ✅ Live |
| Automatic read/write | ✅ Live |
| Vector similarity search | 🔵 Coming Soon |
| Per-user namespaces | 🔵 Coming Soon |
| Knowledge base ingestion | 🔵 Coming Soon |

## Direct access (advanced)

```python
from cognos.memory import Memory

mem = Memory(agent_name="my-agent")

# Write
mem.write("user-pref-123", "Prefers Python, works on crypto infra")

# Read
value = mem.read("user-pref-123")

# Search (Coming Soon)
results = mem.search("user coding preferences", top_k=5)

# List all
items = mem.list()

# Delete
mem.delete("user-pref-123")
```

## Namespaces

Use namespaces to scope memory per user, session, or feature:

```python
mem.write("theme", "dark", namespace="user-42")
mem.write("theme", "light", namespace="user-99")

value = mem.read("theme", namespace="user-42")  # → "dark"
```
