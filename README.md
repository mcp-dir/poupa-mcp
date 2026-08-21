# Poupa AI

### Poupa AI para Claude, ChatGPT e agentes de IA

Finanças pessoais do Poupa AI. Leia saldo agrupado por banco/categoria/cartão/mês, transações por intervalo e palavra-chave, lista de bancos, cartões e categorias; registre, atualize ou apague transações (uma a uma ou em lote) e movimente entre suas contas. Autentique com a sua API key do Poupa AI.

- 📊 **13 ferramentas**
- ✏️ **Leitura e escrita**
- 💬 **Funciona com qualquer cliente MCP**: Claude Desktop, Cursor, VS Code, Cline, Continue
- 🔑 **Login via magic-link (sem senha)**

[English version](README.en.md) · [Documentação completa](docs/) · [Skill pra agentes](skills/)

---

## Instalar em 1 clique

### Claude (Web e Desktop)

A Anthropic unificou a instalação de MCPs em `claude.ai/customize/connectors`. **O mesmo link serve pra Claude Web e Claude Desktop** (basta estar logado):

[➕ Abrir no Claude e conectar](https://claude.ai/new?modal=add-custom-connector#settings/customize-connectors)

**Manual** (se o deeplink não abrir): [claude.ai/customize/connectors](https://claude.ai/customize/connectors?surface=cowork) → **+** → **Adicionar conector personalizado** → cole **Nome** `Poupa AI` e **URL** `https://api.mcp.ai/p_poupa`.

### Cursor

[➕ Instalar Poupa AI no Cursor](cursor://anysphere.cursor-deeplink/mcp/install?name=poupa&config=eyJ1cmwiOiJodHRwczovL2FwaS5tY3AuYWkvcF9wb3VwYSJ9)

### VS Code (Copilot Chat)

[➕ Instalar Poupa AI no VS Code](vscode:mcp/install?name=poupa&config=%7B%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Fapi.mcp.ai%2Fp_poupa%22%7D)

### ChatGPT, Manus, OpenClaw e mais 40+ clientes

Funciona em qualquer cliente MCP que suporte **MCP over HTTP**. A URL do servidor é sempre:

```
https://api.mcp.ai/p_poupa
```

Detalhes por cliente: [INSTALL.md](INSTALL.md).

---

## Exemplos de uso

```
Qual o saldo deste mês por categoria?
Lista todas as transações com a palavra Uber nos últimos 30 dias
Registra uma despesa de R$150 hoje no cartão Nubank em alimentação
```

---

## 13 ferramentas disponíveis

| Tool | Descrição |
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

Detalhe de cada tool: [docs/ferramentas.md](docs/ferramentas.md)

---

## Preços

Grátis.

---

## Privacidade & LGPD

- **Sub-processadores**: o LLM host que você escolher (Claude, ChatGPT, Cursor, agente próprio). Lista completa em [docs/privacidade-lgpd.md](docs/privacidade-lgpd.md).
- Os dados retornados pelas tools são enviados ao **LLM host que você escolher**, sub-processador fora do nosso controle. Recomendamos planos com opt-out de treinamento.

---

## Perguntas frequentes

**O servidor é open source?**
O servidor é proprietário (hosted). Este repositório é o wrapper público com manifestos, docs e skills — tudo MIT.

**Posso usar com agente próprio (não Claude/Cursor)?**
Sim — qualquer cliente que suporte MCP over HTTP. URL: `https://api.mcp.ai/p_poupa`.


---

## Suporte

- 📧 [poupa@mcp.ai](mailto:poupa@mcp.ai)
- 🐛 [GitHub Issues](https://github.com/mcp-dir/poupa-mcp/issues)
- 📄 [docs/](docs/)

---

## Licença

MIT — veja [LICENSE](LICENSE). O servidor MCP em `api.mcp.ai/p_poupa` é proprietário (hosted); este repositório (manifestos, docs, skills) é MIT.
