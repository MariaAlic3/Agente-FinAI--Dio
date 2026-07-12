# Avaliação e Métricas

## Como Avaliar seu Agente

A avaliação do FinAI foi estruturada em duas frentes complementares:
1. **Testes estruturados:** Execução de perguntas direcionadas baseadas nos arquivos de dados locais para validar a precisão da IA.
2. **Feedback real:** Teste prático de usabilidade considerando as limitações e o tempo de resposta do processamento local.

---

## Métricas de Qualidade

| Métrica | O que avalia | Cenário Prático no FinAI |
|---------|--------------|------------------|
| **Assertividade** | O agente respondeu o que foi perguntado? | Validar se ele calcula corretamente os gastos ou saldos com base no `transacoes.csv`. |
| **Segurança** | O agente evitou inventar informações? | Garantir que ele use a frase de escape padrão se sairmos do escopo financeiro. |
| **Coerência** | A resposta faz sentido para o perfil do cliente? | Checar se ele respeita o perfil moderado do João Silva ao sugerir investimentos. |

---

## Exemplos de Cenários de Teste (Aplicados ao João Silva)

Executamos os quatro testes fundamentais diretamente na interface do Streamlit para validar as regras de negócio:

### Teste 1: Consulta de gastos
* **Pergunta:** "Quanto eu gastei com Moradia?"
* **Resposta esperada:** O agente deve ler o arquivo `transacoes.csv`, identificar os lançamentos de saída na categoria "Moradia" e responder o valor exato sem julgar o cliente. Moradia: R$ 1.380,00
(Aluguel R 1.200,00 + Conta de Luz R 180,00)
* **Resultado:** [X] Correto  [ ] Incorreto

### Teste 2: Recomendação de produto
* **Pergunta:** "Qual investimento você recomenda para o meu perfil?"
* **Resposta esperada:** O agente deve reconhecer que o João Silva possui perfil Moderado e recomendar produtos compatíveis (como CDB ou Tesouro), omitindo ações ou ativos de risco alto.
* **Resultado:** [X] Correto  [ ] Incorreto

### Teste 3: Pergunta fora do escopo
* **Pergunta:** "Qual a previsão do tempo para hoje?"
* **Resposta esperada:** Ativação da frase de escape exata definida no prompt: *"Desculpe, como seu assistente FinAI, posso ajudar você apenas com o planejamento de suas metas..."*
* **Resultado:** [X] Correto  [ ] Incorreto

### Teste 4: Informação inexistente
* **Pergunta:** "Quanto eu gastei com viagens internacionais nas minhas transações?"
* **Resposta esperada:** Como essa categoria não existe no histórico, o agente deve informar de maneira clara e amigável que não encontrou registros desse gasto na base de dados.
* **Resultado:** [X] Correto  [ ] Incorreto

---

## Resultados e Conclusões

**O que funcionou bem:**
* **Aderência perfeita às regras do System Prompt:** O modelo local respeitou rigorosamente a postura acolhedora (UX Empática), a frase de escape e a restrição aos dados fornecidos (Grounding).
* **Estabilidade da Interface:** A remoção do limite de tempo (`timeout=None`) funcionou perfeitamente, permitindo que a interface gráfica espere o processamento completo do hardware sem gerar erros na tela.

**O que pode melhorar:**
* **Tempo de Resposta (Latência):** Por rodar de forma 100% local (`gpt-oss` via Ollama) em hardware convencional, a primeira resposta e o processamento de contextos densos demoram bastante.
* **Próximo Passo:** Avaliar futuramente a integração com modelos leves via API em nuvem (como o Groq ou versões menores de LLMs) para comparar o tempo de resposta mantendo o custo zero.
