
---

## 4) `docs/04-metricas.md`

```md
# Avaliação e Métricas

## Como Avaliar seu Agente
A avaliação foi feita com testes estruturados e feedback de usuários simulados. Em cada teste, foi verificado se a resposta era correta, segura e coerente com o perfil do cliente.

---

## Métricas de Qualidade

| Métrica | O que avalia | Exemplo de teste |
|---------|--------------|------------------|
| Assertividade | Respondeu corretamente ao que foi perguntado? | Consultar o saldo e receber o valor correto |
| Segurança | Evitou inventar dados? | Perguntar algo fora do escopo e receber uma recusa adequada |
| Coerência | A resposta combina com o perfil do cliente? | Sugerir opção conservadora para perfil conservador |

---

## Exemplos de Cenários de Teste

### Teste 1: Consulta de gastos
- **Pergunta:** "Quanto gastei com alimentação?"
- **Resposta esperada:** Valor baseado no `transacoes.csv`
- **Resultado:** [x] Correto [ ] Incorreto

### Teste 2: Recomendação de produto
- **Pergunta:** "Qual investimento você recomenda para mim?"
- **Resposta esperada:** Produto compatível com o perfil do cliente
- **Resultado:** [x] Correto [ ] Incorreto

### Teste 3: Pergunta fora do escopo
- **Pergunta:** "Qual a previsão do tempo?"
- **Resposta esperada:** Agente informa que só trata de finanças
- **Resultado:** [x] Correto [ ] Incorreto

### Teste 4: Informação inexistente
- **Pergunta:** "Quanto rende o produto XYZ?"
- **Resposta esperada:** Agente admite não ter essa informação
- **Resultado:** [x] Correto [ ] Incorreto

---

## Resultados

**O que funcionou bem:**
- Respostas diretas e compatíveis com o perfil do cliente.
- Boa recusa em perguntas fora do escopo.
- Personalização com base na base de conhecimento.

**O que pode melhorar:**
- Reduzir respostas genéricas.
- Incluir mais exemplos de edge cases.
- Melhorar a explicação de produtos financeiros.

---

## Métricas Avançadas
- Tempo médio de resposta.
- Taxa de respostas sem alucinação.
- Consumo de tokens por interação.
- Taxa de erro na leitura dos arquivos de dados.
