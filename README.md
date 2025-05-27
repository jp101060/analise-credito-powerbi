# Analise-de-Risco-de-Credito-e-Probabilidade-de-Inadimplencia
# 📊 Projeto de Análise de Risco de Crédito com Power BI e PostgreSQL

Este projeto tem como objetivo aplicar técnicas de análise de dados para identificar riscos de inadimplência, oportunidades de upsell e segmentações financeiras, utilizando um dataset fictício de empréstimos.

---

## 🗃️ Base de Dados

- **Fonte**: [Kaggle - Loan Default Prediction](https://www.kaggle.com/datasets/kmldas/loan-default-prediction)
- **Formato Original**: CSV
- **Banco de Dados**: PostgreSQL (`loan_risk`)

---

## ⚙️ Pipeline Inicial

### 📥 Importação do CSV para PostgreSQL (via Python)

```python
import pandas as pd
import psycopg2
from sqlalchemy import create_engine
import os

current_dir = os.getcwd()
file_path = os.path.join(current_dir, "Default_Fin.csv")

df = pd.read_csv(file_path)

engine = create_engine("postgresql+psycopg2://usuário:senha@localhost:5432/loan_risk")
df.to_sql("loans", engine, if_exists="replace", index=False)

print("Dados importados para o PostgreSQL!")


📈 Conexão ao Power BI
Após a importação, a base loan_risk foi conectada ao Power BI para as etapas de transformação, análise e visualização.

🔄 Tratamento de Dados (ETL)
Conversão de colunas categóricas e booleanas.

Padronização de valores monetários como decimais fixos.

Identificação de outliers com base no IQR.

📊 Exemplo de DAX para Outliers
dax
Copiar
Editar
Q1 Salary = PERCENTILEX.INC(ALL('public loans'),'public loans'[Salário anual], 0.25)
Q3 Salary = PERCENTILEX.INC(ALL('public loans'), 'public loans'[Salário anual], 0.75)
IQR Salary = [Q3 Salary] - [Q1 Salary]

Limite Inferior = [Q1 Salary] - 1.5 * [IQR Salary]
Limite Superior = [Q3 Salary] + 1.5 * [IQR Salary]

Outlier Salário = IF('public loans'[Salário anual] < [Limite Inferior] || 'public loans'[Salário anual] > [Limite Superior], "Sim", "Não")
🧠 Enriquecimento de Dados
✅ Colunas Criadas
Faixa de Renda (baixa, média, alta)

Nível de Saldo Bancário (negativo, baixo, alto)

Perfil Financeiro (conservador, endividado, equilibrado)

Score de Risco Simples

Score de Upsell

Potencial de Investimento

Prioridade de Ação

🎯 Métricas Criadas
Taxa de Inadimplência

Perda Financeira Estimada

% de Clientes em Risco

% de Clientes em Risco Crítico

Potencial Top 10 Clientes Premium

📊 Dashboards Criados
Análise de Risco de Crédito

Oportunidades e Upsell

A base visual foi estruturada inicialmente no PowerPoint para melhor estética, e os gráficos foram desenvolvidos e mantidos no Power BI para garantir interatividade.

🔍 Insights Gerados
📉 Análise de Risco
Alta taxa de inadimplência → revisar políticas de crédito.

30% dos clientes em risco → campanhas de renegociação e educação financeira.

Perdas estimadas significativas → ações de recuperação urgentes.

Risco concentrado em baixa/média renda → oferta de produtos acessíveis.

Clientes com alto saldo em risco → abordagem individualizada.

📈 Oportunidades e Upsell
Domínio de perfis conservador/equilibrado → comunicação personalizada.

Alto potencial concentrado em poucos clientes → programas de fidelização.

Clientes de alta renda com potencial de upsell → foco comercial ativo.

Saldos altos com alto potencial de investimento → consultoria dedicada.

🚧 Reflexões e Próximos Passos
A lógica de tratamento de outliers será migrada para Python (melhor performance).

Pretendo automatizar o pipeline com Apache Airflow.

Estudar hospedagem em nuvem (AWS ou Azure) para substituir banco local.

Com datasets reais e mais robustos, aplicar modelos de Machine Learning para previsão de inadimplência.

Reaproveitar este modelo com outras bases, tornando o processo mais automatizado e escalável.

🧠 Conclusão
Apesar das limitações da base (ex.: 97% de inadimplência), o projeto se mostrou uma excelente oportunidade para aplicar conceitos de:

ETL

Modelagem de Indicadores

Análise exploratória

Visualização de dados interativa

Este projeto continuará evoluindo com novos aprendizados, dados e ferramentas.

📁 Arquivos
Default_Fin.csv: base original (não incluída por política de uso do Kaggle, mas o link para acesso ao dataset está disponível)

loan_risk.sql: estrutura do banco 

Dashboards no Power BI (.pbix)

Slides de estrutura visual (.pptx)

Autor: João Pedro Chagas Carvalho Soares
Contato: LinkedIn • GitHub
