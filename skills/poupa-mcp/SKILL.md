---
name: poupa-mcp
description: Skill da REST API do Poupa AI na MCP.AI: 13 endpoints em /api/poupa. Finanças pessoais do Poupa AI. Leia saldo agrupado por banco/categoria/cartão/mês, transações por intervalo e palavra-chave, lista de bancos, cartões e categorias; registre, atualize ou apague transações (uma a uma ou em lote) e movimente entre suas contas. Autentique com a sua API key do Poupa AI. Autentique com workspace API key (sk_live) gerada em app.mcp.ai/settings/api-keys. Use quando o usuário pedir algo coberto pelos endpoints.
---

# Poupa AI — REST API skill

Você tem acesso à **Poupa AI** REST API na MCP.AI.

> Finanças pessoais do Poupa AI. Leia saldo agrupado por banco/categoria/cartão/mês, transações por intervalo e palavra-chave, lista de bancos, cartões e categorias; registre, atualize ou apague transações (uma a uma ou em lote) e movimente entre suas contas. Autentique com a sua API key do Poupa AI.

## Base URL

```
https://api.mcp.ai/api/poupa
```

Todo endpoint é um **POST** na Base URL + o path abaixo. Os parâmetros vão no corpo JSON.

## Autenticação

Inclua em toda request:

```
Authorization: Bearer sk_live_...
Content-Type: application/json
```

> Gere sua chave em **https://app.mcp.ai/settings/api-keys** (workspace API key `sk_live_…`, não expira, revogável). Uma única chave serve pra todos os seus MCPs.

## Formato de resposta

```json
{ "ok": true, "tool": "<tool_id>", "result": <payload> }
```

## Exemplo cURL

```bash
curl -X POST https://api.mcp.ai/api/poupa/add/transaction \
  -H "Authorization: Bearer sk_live_..." \
  -H "Content-Type: application/json" \
  -d '{"value":0,"date":"..."}'
```

## Reportar problemas

Se um endpoint retornar erro, vazio ou dado inesperado, reporte (não desista calado): **POST /api/poupa/report** com `{ "message": "...", "context"?: "...", "conversation"?: [...] }`. Isso notifica o time da MCP.AI.

## Endpoints (13)

#### `poupa_add_transaction`

Cria uma transação. value e date são obrigatórios; demais campos opcionais. Para parcelar, use installments; para recorrer, use expense_recurrency (dias) OU recurrency_array_dates (lista de datas). _(POST /api/poupa/add/transaction)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `value` | number | Sim | Valor (positivo = entrada, negativo = saída). |
| `date` | string | Sim | Data no formato YYYY-MM-DD. |
| `description` | string | Não | Descrição da transação. |
| `category` | string | Não | Nome da categoria. |
| `payment_bank` | string | Não | Banco/pagador. |
| `card_name` | string | Não | Cartão (se aplicável). |
| `installments` | number | Não | Parcelas (>=2 cria a série; 1 = single). |
| `expense_recurrency` | number | Não | Recorrência em dias (ex.: 30 = mensal). |
| `recurrency_array_dates` | string[] | Não | Lista de datas YYYY-MM-DD pra agendar várias ocorrências. |

#### `poupa_add_transactions`

Cria várias transações de uma vez (bulk). _(POST /api/poupa/add/transactions)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `transactions` | object[] | Sim | Lista de transações a criar. |

#### `poupa_banks`

Lista os bancos/contas do usuário. _(POST /api/poupa/banks)_

#### `poupa_cards`

Lista os cartões de crédito do usuário. _(POST /api/poupa/cards)_

#### `poupa_category`

Lista as categorias do usuário. _(POST /api/poupa/category)_

#### `poupa_defaults`

Categorias e métodos de pagamento padrão do usuário. _(POST /api/poupa/defaults)_

#### `poupa_delete_transactions_by_filter`

Deleta transações por filtro. O filtro precisa ser não vazio (a tool se recusa a deletar tudo). Aceita ids, intervalo de datas, descrição, categoria, etc. _(POST /api/poupa/delete/transactions/by/filter)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `ids` | string[] | Não | IDs específicos. |
| `start_date` | string | Não | Início (YYYY-MM-DD). |
| `end_date` | string | Não | Fim (YYYY-MM-DD). |
| `description` | string | Não | Trecho da descrição. |
| `category` | string | Não | Nome da categoria. |

#### `poupa_get_balance`

Saldo do usuário, agrupado por banco, categoria, método de pagamento, cartão, tipo (entrada/saída) e mês. _(POST /api/poupa/get/balance)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `start_date` | string | Não | Início (YYYY-MM-DD). |
| `end_date` | string | Não | Fim (YYYY-MM-DD). |

#### `poupa_memories`

Memórias/notas do usuário gravadas no Poupa AI. _(POST /api/poupa/memories)_

#### `poupa_preferences`

Preferências do usuário (idioma, moeda, etc.). _(POST /api/poupa/preferences)_

#### `poupa_retrieve_transactions`

Lista transações no intervalo (YYYY-MM-DD), opcionalmente filtradas por palavras-chave (match parcial case-insensitive na descrição), cartão e/ou banco/pagador. _(POST /api/poupa/retrieve/transactions)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `start_date` | string | Não | Início (YYYY-MM-DD). |
| `end_date` | string | Não | Fim (YYYY-MM-DD). |
| `keywords` | string[] | Não | Palavras-chave a buscar na descrição. |
| `card_name` | string | Não | Nome do cartão. |
| `payment_bank` | string | Não | Banco ou método de pagamento. |

#### `poupa_transfer_between_banks`

Registra uma transferência entre dois bancos/contas do PRÓPRIO usuário (movimento contábil — não executa transferência bancária real). _(POST /api/poupa/transfer/between/banks)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `from_bank` | string | Sim | Banco/conta de origem. |
| `to_bank` | string | Sim | Banco/conta de destino. |
| `value` | number | Sim | Valor a transferir. |
| `date` | string | Não | Data (YYYY-MM-DD), opcional. |

#### `poupa_update_transactions`

Atualiza uma ou mais transações existentes. _(POST /api/poupa/update/transactions)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `ids` | string[] | Não | IDs das transações a atualizar. |
| `filter` | object | Não | Filtro alternativo (description, date range, category, etc.). |
| `changes` | object | Não | Campos a alterar. |

---

Este MCP também funciona via **conexão MCP** (Claude / Cursor) em `https://api.mcp.ai/p_poupa` — veja o [README](../../README.md). A skill acima é pra consumir a **REST API** direto (agente próprio / código).
