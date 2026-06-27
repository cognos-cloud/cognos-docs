# Tools

Tools connect agents to external services. Pass tool names to the `tools` parameter and Cognos Cloud handles authentication, rate limiting, and error handling automatically.

---

## Available now

| Tool | Description |
|---|---|
| `web` | Search the web and fetch page content |
| `slack` | Post messages, read channels, manage threads |
| `github` | Read/write PRs, issues, code, comments |
| `discord` | Send messages, manage channels |
| `postgresql` | Query and write to PostgreSQL databases |
| `notion` | Read/write pages and databases |
| `gmail` | Send and read emails |
| `stripe` | Manage payments, invoices, customers (read-only by default) |
| `solana` | Check balances, fetch transactions, simulate txs |
| `ethereum` | Check balances, fetch transactions, simulate txs |

---

## Usage

```python
agent = Agent(
    name="my-agent",
    tools=["web", "slack", "github"],
)
```

---

## Custom tools

Register any Python function as a tool using the `@tool` decorator:

```python
from cognos import tool

@tool(name="send-invoice", description="Sends an invoice via your internal billing API")
def send_invoice(customer_id: str, amount_usd: float) -> str:
    response = requests.post("https://api.yourapp.com/invoices", json={
        "customer_id": customer_id,
        "amount": amount_usd,
    })
    return f"Invoice sent: {response.json()['invoice_id']}"

agent = Agent(
    name="billing-agent",
    tools=[send_invoice],
)
```

### Rules for custom tools

1. Parameters must be typed (`str`, `int`, `float`, `bool`)
2. Return type must be `str`
3. The function must be importable from the project root
4. Keep tool functions fast — under 10 seconds per call

---

## Coming soon

| Tool | Status |
|---|---|
| `linear` | Coming Soon |
| `jira` | Coming Soon |
| `hubspot` | Coming Soon |
| `salesforce` | Coming Soon |
| `twilio` | Coming Soon |
