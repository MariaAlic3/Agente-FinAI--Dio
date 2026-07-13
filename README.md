# 💰 FinAI — Mentor Financeiro Inteligente com IA Generativa Local

[![Python](https://img.shields.io/badge/Python-3.14-blue.svg)](https://www.python.org/)
[![Streamlit](https://img.shields.io/badge/Framework-Streamlit-FF4B4B.svg)](https://streamlit.io/)
[![Ollama](https://img.shields.io/badge/LLM-gpt--oss%20(Local)-000000.svg)](https://ollama.ai/)

O **FinAI** é um agente financeiro consultivo e inteligente desenvolvido para transformar dados financeiros brutos em uma jornada de planejamento leve, humana e altamente personalizada. O projeto foi construído do zero como parte do desafio prático de Automação de Dados com IA (DIO / Afya / Programadores do Amanhã).

Diferente de chatbots tradicionais e frios, o FinAI atua como um mentor proativo e empático, utilizando modelos de linguagem de código aberto rodando de forma 100% local para garantir a privacidade absoluta dos dados bancários do usuário.

---

## 🎯 Caso de Uso e Dor Resolvida

Muitas pessoas abandonam o planejamento orçamentário por enfrentarem interfaces complexas ou abordagens robóticas e punitivas sobre seus hábitos de consumo. 

O FinAI resolve esse problema ao atuar como um **mentor financeiro empático e consultivo**. Ele consome dados consolidados do cliente para extrair insights precisos sobre o orçamento e guiar o planejamento de metas ativas de forma estritamente matemática, técnica e acolhedora — eliminando completamente qualquer viés de julgamento (*UX Empática*).

---

## 🛠️ Stack Tecnológica & Arquitetura

A solução foi desenhada para rodar localmente com custo zero de infraestrutura e máxima proteção de dados:

*   **Interface do Usuário:** Interface de chat interativa desenvolvida com **Streamlit**.
*   **Orquestração e Dados:** **Pandas** e **JSON** para o carregamento e injeção dinâmica da base de conhecimento em memória.
*   **Engine de IA:** **Ollama** servindo o modelo local `gpt-oss` via requisições HTTP (`requests`).

### 📦 Estrutura do Repositório

📁 FinAi/ 
│ 
├── 📄 README.md                      # Esta documentação estratégica
│ 
├── 📁 data/                           # Base de conhecimento local (Mockada)
│   ├── perfil_investidor.json        # Dados de perfil, metas e tolerância a risco
│   ├── transacoes.csv                # Histórico de lançamentos e consumo
│   ├── historico_atendimento.csv     # Histórico de interações anteriores
│   └── produtos_financeiros.json     # Catálogo de produtos e serviços disponíveis
│ 
├── 📁 docs/                           # Detalhamento das etapas de engenharia
│   ├── 01-documentacao-agente.md
│   ├── 02-base-conhecimento.md
│   ├── 03-prompts.md
│   └── 04-metricas.md
│ 
└── 📁 src/                            # Código-fonte da aplicação
└── app.py                        # Script principal do ecossistema Streamlit


---

## 🧠 Engenharia de Prompts e Engenharia de Segurança

O comportamento do FinAI foi blindado via *System Prompt* estruturado sob quatro pilares fundamentais:

1.  **Postura Sem Julgamentos:** O agente avalia gastos sob uma ótica estritamente técnica e matemática. Palavras como "errado" ou "irresponsável" são proibidas.
2.  **Grounding Absoluto (Anti-Alucinação):** A IA é restrita a responder perguntas baseando-se unicamente nas tabelas e perfis injetados da pasta `data/`. Ela não inventa produtos ou taxas inexistentes.
3.  **Mecanismo de Escape (Edge Cases):** Perguntas fora do escopo de finanças disparam uma frase de escape padronizada para manter a segurança do fluxo de atendimento.
4.  **Concisão e Acessibilidade:** Respostas estruturadas em tópicos curtos de Markdown, utilizando uma linguagem inclusiva e livre de jargões complexos.

---

## ⚡ Resiliência e Engenharia de Infraestrutura Local

Durante os testes em ambiente com hardware convencional, identificou-se uma alta latência no processamento inicial do modelo local `gpt-oss`. 

**Solução Aplicada:** O código foi otimizado removendo o limite de espera HTTP padrão (`timeout=None`). Com isso, a aplicação do Streamlit ganhou resiliência, aguardando de forma estável o processamento completo do modelo local sem apresentar quebras ou travamentos de tela para o usuário, garantindo uma experiência de uso contínua.

---

## 🧪 Avaliação e Casos de Teste

O agente foi submetido a uma esteira de testes estruturados de qualidade:

*   **Teste de Assertividade (Consulta de Gastos):** Validou com sucesso os cálculos de categorias do arquivo `transacoes.csv`.
*   **Teste de Coerência (Recomendação):** Recomendou apenas produtos adequados ao perfil moderado do cliente fictício (João Silva), ignorando ativos de alto risco.
*   **Teste de Segurança (Inexistência e Escopo):** Negou com sucesso perguntas de escopo externo (previsão do tempo) usando a frase de escape regulamentada.

---

## 🎬 Assista ao meu Pitch e Demonstração

Gravei uma apresentação executiva em estilo *Pitch* de 3 minutos resumindo o modelo de negócios, a arquitetura e exibindo a tela da IA funcionando na prática.

🔗 https://youtu.be/gndPfIeLcu0

---

### 🚀 Como Executar o Projeto Localmente

1. Certifique-se de ter o **Ollama** instalado e inicie o modelo no terminal:
   ```bash
   ollama run gpt-oss
Execute o Streamlit apontando para o interpretador do seu ambiente:

Bash
python -m streamlit run src/app.py

