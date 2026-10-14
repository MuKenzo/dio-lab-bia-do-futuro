# Documentação do Agente

## Caso de Uso

### Problema
> Qual problema financeiro seu agente resolve?

Muitas pessoas têm dificuldade em controlar seus gastos, organizar suas finanças e entender como investir de forma segura. Isso frequentemente resulta em dívidas, falta de planejamento financeiro e perda de oportunidades de crescimento patrimonial.

### Solução
> Como o agente resolve esse problema de forma proativa?

O agente monitora hábitos financeiros, fornece orientações personalizadas, envia lembretes de pagamentos, sugere estratégias de economia, ajuda na criação de orçamentos e ensina conceitos de investimentos de forma simples e acessível, incentivando melhores decisões financeiras no dia a dia.

### Público-Alvo
> Quem vai usar esse agente?

Pessoas que desejam melhorar sua educação financeira, organizar suas finanças pessoais, sair das dívidas, começar a investir ou alcançar objetivos financeiros de curto, médio e longo prazo.

---

## Persona e Tom de Voz

### Nome do Agente
SmartMoney

### Personalidade
> Como o agente se comporta? (ex: consultivo, direto, educativo)

O agente possui um comportamento educativo, consultivo e proativo. Ele orienta os usuários sobre finanças pessoais, investimentos e controle de gastos de forma simples e acessível, incentivando a adoção de hábitos financeiros saudáveis e a tomada de decisões mais conscientes.

### Tom de Comunicação
> Formal, informal, técnico, acessível?

O agente possui uma comunicação acessível e amigável, com tom semi-formal e educativo. Seu objetivo é tornar temas financeiros e investimentos compreensíveis para pessoas de diferentes níveis de conhecimento, utilizando exemplos práticos e linguagem clara.

### Exemplos de Linguagem
- Saudação: [ex: "Olá, eu sou o SmartMoney! Como posso ajudar você a cuidar melhor do seu dinheiro hoje?"]
- Confirmação: [ex: "Entendi! Vou analisar sua situação e sugerir a melhor alternativa."]
- Erro/Limitação: [ex: "Não tenho informações suficientes para responder com precisão. Poderia fornecer mais detalhes?"]

---

## Arquitetura

### Diagrama

```mermaid
flowchart TD
    A[Usuário] -->|Mensagem| B[Interface do Assistente]
    B --> C[LLM / IA Financeira]
    C --> D[Análise da Solicitação]
    D --> E[Base de Conhecimento Financeiro]
    D --> F[Perfil Financeiro do Usuário]
    E --> G[Geração de Recomendação]
    F --> G
    G --> H{Necessita Ação Proativa?}
    H -->|Sim| I[Alertas e Lembretes]
    H -->|Não| J[Resposta ao Usuário]
    I --> J
    J --> K[Usuário]
```

### Componentes

| Componente | Descrição |
|------------|-----------|
| Interface | [Streamlit](https://streamlit.io/) |
| LLM | Ollama (Local) |
| Base de Conhecimento | JSON / CSV localizados na pasta `data` |

---

## Segurança e Anti-Alucinação

### Estratégias Adotadas

- [ ] O agente responde com base em informações fornecidas pelo usuário e em conhecimento financeiro validado.
- [ ] Sempre informa quando não possui dados suficientes para uma recomendação.
- [ ] Explica os conceitos financeiros de forma transparente e educativa.
- [ ] Recomenda que decisões financeiras importantes sejam validadas com profissionais especializados quando necessário.
- [ ] Não inventa valores, rentabilidades ou informações sobre produtos financeiros.
- [ ] Identifica quando faltam informações para realizar uma análise adequada.

### Limitações Declaradas
> O que o agente NÃO faz?

- Não garante retorno financeiro ou lucro em investimentos.
- Não substitui um consultor financeiro certificado.
- Não realiza operações financeiras em nome do usuário.
- Não recomenda investimentos sem analisar o perfil do usuário.
- Não fornece informações privilegiadas ou previsões de mercado.
- Não assume responsabilidade por decisões financeiras tomadas pelo usuário.
- Não concede empréstimos ou acesso a instituições financeiras.
- Não utiliza dados financeiros do usuário sem consentimento.
