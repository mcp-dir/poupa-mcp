# Poupa AI

### Poupa AI for Claude, ChatGPT and AI agents

Personal finance by Poupa AI. Read balance grouped by bank/category/card/month, transactions filtered by date and keyword, plus banks, cards and categories; create, update or delete transactions (one by one or in bulk) and move money between your own accounts. Authenticate with your Poupa AI API key.

- 📊 **13 tools**
- ✏️ **Read and write**
- 💬 **Works with any MCP client**: Claude Desktop, Cursor, VS Code, Cline, Continue
- 🔑 **Magic-link login (no password)**

[Portuguese version](README.md) · [Full docs (PT-BR)](docs/)

---

## One-click install

### Claude (Web and Desktop)

[➕ Open in Claude and connect](https://claude.ai/new?modal=add-custom-connector#settings/customize-connectors)

Manual: [claude.ai/customize/connectors](https://claude.ai/customize/connectors?surface=cowork) → **+** → **Add custom connector** → name `Poupa AI`, URL `https://api.mcp.ai/p_poupa`.

### Cursor

[➕ Install in Cursor](cursor://anysphere.cursor-deeplink/mcp/install?name=poupa&config=eyJ1cmwiOiJodHRwczovL2FwaS5tY3AuYWkvcF9wb3VwYSJ9)

### VS Code (Copilot Chat)

[➕ Install in VS Code](vscode:mcp/install?name=poupa&config=%7B%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Fapi.mcp.ai%2Fp_poupa%22%7D)

### Any other MCP-over-HTTP client

```
https://api.mcp.ai/p_poupa
```

---

## 13 tools

| Tool | Description |
|---|---|
| `poupa_get_balance` | Saldo do usuário, agrupado por banco, categoria, método de pagamento, cartão, tipo (entrada/saída) e mês. |
| `poupa_retrieve_transactions` | Lista transações no intervalo (YYYY-MM-DD), opcionalmente filtradas por palavras-chave (match parcial case-insensitive na descrição), cartão e/ou banco/pagador. |
| `poupa_banks` | Lista os bancos/contas do usuário. |
| `poupa_cards` | Lista os cartões de crédito do usuário. |
| `poupa_category` | Lista as categorias do usuário. |
| `poupa_preferences` | Preferências do usuário (idioma, moeda, etc.). |
| `poupa_defaults` | Categorias e métodos de pagamento padrão do usuário. |
| `poupa_memories` | Memórias/notas do usuário gravadas no Poupa AI. |
| `poupa_add_transaction` | Cria uma transação. value e date são obrigatórios; demais campos opcionais. Para parcelar, use installments; para recorrer, use expense_recurrency (dias) OU recurrency_array_dates (lista de datas). |
| `poupa_add_transactions` | Cria várias transações de uma vez (bulk). |
| `poupa_update_transactions` | Atualiza uma ou mais transações existentes. |
| `poupa_delete_transactions_by_filter` | Deleta transações por filtro. O filtro precisa ser não vazio (a tool se recusa a deletar tudo). Aceita ids, intervalo de datas, descrição, categoria, etc. |
| `poupa_transfer_between_banks` | Registra uma transferência entre dois bancos/contas do PRÓPRIO usuário (movimento contábil — não executa transferência bancária real). |

---

## Pricing

Free.

---

## License

MIT — see [LICENSE](LICENSE). The MCP server at `api.mcp.ai/p_poupa` is proprietary (hosted); this repo (manifests, docs, skills) is MIT.
