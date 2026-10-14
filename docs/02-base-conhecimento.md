# Base de Conhecimento

## Dados Utilizados

| Arquivo | Formato | Para que serve no SmartMoney? |
|---------|---------|---------------------|
| `historico_atendimento.csv` | CSV | Contextualizar interações anteriores, ou seja, dar continuidade no atendimento de forma mais eficiente. |
| `perfil_investidor.json` | JSON | Personalizar as recomendações e fornecer as explicações necessárias para o aprendizado do usuário. |
| `produtos_financeiros.json` | JSON | Sugerir produtos e fornecer dicas ao usuário, de acordo com a sua situação. |
| `transacoes.csv` | CSV | Analisar padrão de gastos do cliente e usar essas informações de forma didática. |

---

## Adaptações nos Dados

O produto Fundo Imobiliário (FII) substituiu o Fundo Multimercado, pois, pessoalmente, me sinto mais confiante em utilizar produtos financeiro que eu conheço. Dessa forma, o SmartMoney conseguirá validar as respostas de uma forma mais assertiva.

---

## Estratégia de Integração

### Como os dados são carregados?
Existem 2 possibilidades:

- Injetar os dados diretamente no prompt;
- Carregar os arquivos via código.

```python
import pandas as pd
import json

# CSVs
historico = pd.read_csv('data/historico_atendimento.csv')
transacoes = pd.read_csv('data/transacoes.csv')

# JSONs
with open('data/perfil_investidor.json', 'r', encoding='utf-8') as f:
  perfil = json.load(f)

with open('data/produtos_financeiros.json', 'r', encoding='utf-8') as f:
  produtos = json.load(f)
```

### Como os dados são usados no prompt?
```text
DADOS DO CLIENTE + PERFIL (data/perfil_investidor.json):
{
  "nome": "João Silva",
  "idade": 32,
  "profissao": "Analista de Sistemas",
  "renda_mensal": 5000.00,
  "perfil_investidor": "moderado",
  "objetivo_principal": "Construir reserva de emergência",
  "patrimonio_total": 15000.00,
  "reserva_emergencia_atual": 10000.00,
  "aceita_risco": false,
  "metas": [
    {
      "meta": "Completar reserva de emergência",
      "valor_necessario": 15000.00,
      "prazo": "2026-06"
    },
    {
      "meta": "Entrada do apartamento",
      "valor_necessario": 50000.00,
      "prazo": "2027-12"
    }
  ]
}

TRANSAÇÕES DO CLIENTE (data/transacoes.csv):
data,descricao,categoria,valor,tipo
2025-10-01,Salário,receita,5000.00,entrada
2025-10-02,Aluguel,moradia,1200.00,saida
2025-10-03,Supermercado,alimentacao,450.00,saida
2025-10-05,Netflix,lazer,55.90,saida
2025-10-07,Farmácia,saude,89.00,saida
2025-10-10,Restaurante,alimentacao,120.00,saida
2025-10-12,Uber,transporte,45.00,saida
2025-10-15,Conta de Luz,moradia,180.00,saida
2025-10-20,Academia,saude,99.00,saida
2025-10-25,Combustível,transporte,250.00,saida

HISTÓRICO DE ATENDIMENTO DO CLIENTE (data/historico_atendimento.csv):
data,canal,tema,resumo,resolvido
2025-09-15,chat,CDB,Cliente perguntou sobre rentabilidade e prazos,sim
2025-09-22,telefone,Problema no app,Erro ao visualizar extrato foi corrigido,sim
2025-10-01,chat,Tesouro Selic,Cliente pediu explicação sobre o funcionamento do Tesouro Direto,sim
2025-10-12,chat,Metas financeiras,Cliente acompanhou o progresso da reserva de emergência,sim
2025-10-25,email,Atualização cadastral,Cliente atualizou e-mail e telefone,sim

PRODUTOS DISPONÍVEIS PARA ENSINO (data/produtos_financeiros.json):
[
  {
    "nome": "Tesouro Selic",
    "categoria": "renda_fixa",
    "risco": "baixo",
    "rentabilidade": "100% da Selic",
    "aporte_minimo": 30.00,
    "indicado_para": "Reserva de emergência e iniciantes"
  },
  {
    "nome": "CDB Liquidez Diária",
    "categoria": "renda_fixa",
    "risco": "baixo",
    "rentabilidade": "102% do CDI",
    "aporte_minimo": 100.00,
    "indicado_para": "Quem busca segurança com rendimento diário"
  },
  {
    "nome": "LCI/LCA",
    "categoria": "renda_fixa",
    "risco": "baixo",
    "rentabilidade": "95% do CDI",
    "aporte_minimo": 1000.00,
    "indicado_para": "Quem pode esperar 90 dias (isento de IR)"
  },
  {
    "nome": "Fundo Imobiliário (FII)",
    "categoria": "fundo",
    "risco": "alto",
    "rentabilidade": "6% à 12% ao ano",
    "aporte_minimo": 100.00,
    "indicado_para": "Perfil arrojado com foco no longo prazo"
  },
  {
    "nome": "Fundo de Ações",
    "categoria": "fundo",
    "risco": "alto",
    "rentabilidade": "Variável",
    "aporte_minimo": 100.00,
    "indicado_para": "Perfil arrojado com foco no longo prazo"
  }
]
```

---

## Exemplo de Contexto Montado

> Mostre um exemplo de como os dados são formatados para o agente.

```
DADOS DO CLIENTE:

- Nome: João Silva
- Perfil: Moderado
- Objetivo: Construir reserva de emergência
- Reserva Atual: R$ 10.000 (Meta: R$ 15.000)

RESUMO DE GASTOS (Outubro/2026):
- Moradia: R$ 1.300
- Alimentação: R$ 570
- Transporte: R$ 295
- Saúde: R$ 188
- Lazer: R$ 55,90
- Total de Saídas: R$ 2.488,90

PRODUTOS DISPONÍVEIS PARA EXPLICAR:
- Tesouro Selic (Risco Baixo)
- CDB Liquidez Diária (Risco Baixo)
- LCI/LCA (Risco Baixo)
- Fundo Imobiliário (FII) (Risco Alto)
- Fundo de Ações (Risco Alto)
```
