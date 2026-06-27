# API Reference

Every deployed agent automatically gets a REST API endpoint.

**Base URL:** `https://api.cognos.ai/v1`

All requests require:
```
Authorization: Bearer YOUR_API_KEY
Content-Type: application/json
```

Generate API keys from your dashboard at `cloud.cognos.ai`.

---

## Run an agent

```
POST /agents/{name}/run
```

**Request:**
```json
{
  "input": "Research the latest AI safety papers",
  "stream": false,
  "context": {}
}
```

**Response:**
```json
{
  "run_id": "run_01HXZK4R2P...",
  "status": "completed",
  "output": "Here are the top 5 AI safety papers from the last week...",
  "latency_ms": 824,
  "cost_usd": 0.03,
  "memory_writes": 4
}
```

---

## Get agent status

```
GET /agents/{name}
```

**Response:**
```json
{
  "name": "research-agent",
  "status": "running",
  "model": "gpt-4o",
  "memory": true,
  "tools": ["web", "slack"],
  "cron": "0 9 * * *",
  "deployed_at": "2025-01-15T09:00:00Z",
  "last_run_at": "2025-01-22T09:00:00Z"
}
```

---

## Get logs

```
GET /agents/{name}/logs?tail=100
```

**Response:**
```json
{
  "logs": [
    {
      "timestamp": "2025-01-22T09:00:01Z",
      "level": "INFO",
      "message": "Starting scheduled run (cron: 0 9 * * *)"
    }
  ]
}
```

---

## List agents

```
GET /agents
```

**Response:**
```json
{
  "agents": [
    { "name": "research-agent", "status": "running" },
    { "name": "github-agent",   "status": "running" }
  ]
}
```

---

## Start / Stop / Restart

```
POST /agents/{name}/start
POST /agents/{name}/stop
POST /agents/{name}/restart
```

All return `{"status": "ok"}`.

---

## Delete

```
DELETE /agents/{name}
```

Permanently deletes the agent and all its resources including memory.

---

## Status codes

| Code | Meaning |
|---|---|
| 200 | Success |
| 400 | Bad request — check your payload |
| 401 | Unauthorized — check your API key |
| 404 | Agent not found |
| 429 | Rate limited |
| 500 | Server error — contact support |
