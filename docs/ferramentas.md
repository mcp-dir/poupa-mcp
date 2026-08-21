# Ferramentas

Poupa AI expõe 13 ferramentas.

### 1. `poupa_get_balance`
**Input**: `start_date` (opcional), `end_date` (opcional)

Saldo do usuário, agrupado por banco, categoria, método de pagamento, cartão, tipo (entrada/saída) e mês.

### 2. `poupa_retrieve_transactions`
**Input**: `start_date` (opcional), `end_date` (opcional), `keywords` (opcional), `card_name` (opcional), `payment_bank` (opcional)

Lista transações no intervalo (YYYY-MM-DD), opcionalmente filtradas por palavras-chave (match parcial case-insensitive na descrição), cartão e/ou banco/pagador.

### 3. `poupa_banks`
**Input**: nenhum input

Lista os bancos/contas do usuário.

### 4. `poupa_cards`
**Input**: nenhum input

Lista os cartões de crédito do usuário.

### 5. `poupa_category`
**Input**: nenhum input

Lista as categorias do usuário.

### 6. `poupa_preferences`
**Input**: nenhum input

Preferências do usuário (idioma, moeda, etc.).

### 7. `poupa_defaults`
**Input**: nenhum input

Categorias e métodos de pagamento padrão do usuário.

### 8. `poupa_memories`
**Input**: nenhum input

Memórias/notas do usuário gravadas no Poupa AI.

### 9. `poupa_add_transaction`
**Input**: `value`, `date`, `description` (opcional), `category` (opcional), `payment_bank` (opcional), `card_name` (opcional), `installments` (opcional), `expense_recurrency` (opcional), `recurrency_array_dates` (opcional)

Cria uma transação. value e date são obrigatórios; demais campos opcionais. Para parcelar, use installments; para recorrer, use expense_recurrency (dias) OU recurrency_array_dates (lista de datas).

### 10. `poupa_add_transactions`
**Input**: `transactions`

Cria várias transações de uma vez (bulk).

### 11. `poupa_update_transactions`
**Input**: `ids` (opcional), `filter` (opcional), `changes` (opcional)

Atualiza uma ou mais transações existentes.

### 12. `poupa_delete_transactions_by_filter`
**Input**: `ids` (opcional), `start_date` (opcional), `end_date` (opcional), `description` (opcional), `category` (opcional)

Deleta transações por filtro. O filtro precisa ser não vazio (a tool se recusa a deletar tudo). Aceita ids, intervalo de datas, descrição, categoria, etc.

### 13. `poupa_transfer_between_banks`
**Input**: `from_bank`, `to_bank`, `value`, `date` (opcional)

Registra uma transferência entre dois bancos/contas do PRÓPRIO usuário (movimento contábil — não executa transferência bancária real).

## Prompts de exemplo

```
Qual o saldo deste mês por categoria?
Lista todas as transações com a palavra Uber nos últimos 30 dias
Registra uma despesa de R$150 hoje no cartão Nubank em alimentação
```
