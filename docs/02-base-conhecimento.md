# Base de Conhecimento

## Dados Utilizados

| Arquivo | Formato | Utilização no Agente |
|---------|---------|----------------------|
| `historico_atendimento.csv` | CSV | Contextualizar interações anteriores |
| `perfil_investidor.json` | JSON | Personalizar recomendações |
| `produtos_financeiros.json` | JSON | Sugerir produtos adequados ao perfil |
| `transacoes.csv` | CSV | Identificar padrões de gastos e recorrências |


---

## Adaptações nos Dados

> Você modificou ou expandiu os dados mockados? Descreva aqui.

Os dados foram organizados para representar um cliente fictício, com transações, perfil de investidor e histórico de atendimento. Também foram incluídos campos para facilitar a leitura pelo agente, como categoria de gasto, objetivo financeiro e nível de risco.

---

## Estratégia de Integração

### Como os dados são carregados?
> Descreva como seu agente acessa a base de conhecimento.

Os arquivos CSV e JSON são carregados no início da aplicação e transformados em contexto textual para consulta do LLM.

### Como os dados são usados no prompt?
> Os dados vão no system prompt? São consultados dinamicamente?

Os dados são resumidos e inseridos no contexto da conversa para orientar respostas mais precisas. O agente usa essas informações para gerar recomendações compatíveis com o perfil do cliente.

---

## Exemplo de Contexto Montado

> Mostre um exemplo de como os dados são formatados para o agente.

```
Dados do Cliente:
- Nome: João Silva
- Perfil: Moderado
- Objetivo: montar reserva de emergência
- Saldo disponível: R$ 5.000

Últimas transações:
- 01/11: Supermercado - R$ 450
- 03/11: Streaming - R$ 55
- 05/11: Restaurante - R$ 120

Histórico de atendimento:
- Cliente informou que quer reduzir gastos com lazer.
- Cliente pediu sugestão de produto com baixo risco.
...
```
