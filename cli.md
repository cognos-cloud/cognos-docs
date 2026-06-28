# CLI Reference

The Cognos Cloud CLI is installed automatically with the SDK:

```bash
pip install cognos
```

---

## Commands

### `cognos init`

Scaffold a new agent project in the current directory.

```bash
cognos init
```

Creates:
```
my-agent/
  agent.py
  .env.example
  .gitignore
  README.md
```

---

### `cognos login`

Authenticate with Cognos Cloud.

```bash
cognos login
```

Opens a browser for OAuth. Saves token to `~/.cognos/credentials`.

To use an API key instead:
```bash
export COGNOS_API_KEY=your_key_here
```

---

### `cognos dev`

Run the agent locally with hot reload.

```bash
cognos dev
cognos dev agent.py --port 8080
```

Starts a local runtime at `http://localhost:8080/run`. Reloads on file changes.

---

### `cognos deploy`

Deploy the agent in the current directory to Cognos Cloud.

```bash
cognos deploy
cognos deploy --name custom-name
cognos deploy --dry-run
```

Looks for `agent.py` or `cognos.toml` in the current directory.

---

### `cognos logs`

Stream logs from a running agent.

```bash
cognos logs my-agent
cognos logs my-agent --tail 50
cognos logs my-agent --follow
```

| Flag | Default | Description |
|---|---|---|
| `--tail N` | 100 | Show last N lines |
| `--follow / -f` | false | Stream continuously |

---

### `cognos monitor`

Open the agent dashboard in your browser.

```bash
cognos monitor my-agent
```

Opens `https://cognoscloud.xyz/agents/my-agent`.

---

### `cognos restart`

Restart a running agent.

```bash
cognos restart my-agent
```

---

### `cognos rollback`

Roll back to the previous deployment.

```bash
cognos rollback my-agent
```

---

### `cognos delete`

Delete an agent and all its resources. Irreversible.

```bash
cognos delete my-agent
cognos delete my-agent --yes   # skip confirmation
```
