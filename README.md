# 🩺 Insurance Cost Analysis — EDA & Insights

## 🎯 Objetivo
Explorar e compreender os fatores que influenciam os custos de seguro médico (`charges`) em uma base de clientes, 
identificando padrões, correlações e **segmentos de alto custo (top 5%)**. 
O estudo também define estratégias para **predição de propensão de alto custo** e **estimativa contínua de custo futuro**.

---

## 📊 Resumo das Informações

**Fonte dos dados:** `insurance.csv`  
**Total de registros:** 1.338  
**Variáveis principais:**
| Coluna | Tipo | Descrição |
|--------|------|------------|
| age | int | Idade do indivíduo |
| sex | object | Sexo (male/female) |
| bmi | float | Índice de Massa Corporal (IMC) |
| children | int | Número de dependentes |
| smoker | object | Fumante ou não |
| region | object | Região de residência |
| charges | float | Custo total cobrado |

**Qualidade dos dados:**  
Sem valores ausentes. Distribuições contínuas assimétricas, especialmente `charges`.  
3 variáveis categóricas e 4 numéricas.

---

## 📈 Resumo Executivo Visual

| Indicador | Destaque | Insight |
|------------|-----------|----------|
| 💨 **Fumantes** | 5x maior custo médio | Principal fator de risco |
| ⚖️ **IMC** | Aumento após IMC > 30 | Relação não linear com custo |
| 👶 **Idade** | Crescimento contínuo | Relevante após 40 anos |
| 📍 **Região** | Diferenças pequenas | Fator secundário |
| 💰 **Top 5%** | Fumantes com alto IMC e idade > 40 | Segmento prioritário |

---

## 🔍 Testes Estatísticos Utilizados

| Teste | Aplicação | Objetivo |
|-------|------------|-----------|
| **Shapiro-Wilk** | Normalidade | Validar se as distribuições numéricas seguem normalidade |
| **Levene** | Homocedasticidade | Verificar igualdade de variâncias entre grupos |
| **Mann-Whitney U** | Comparação 2 grupos | Comparar fumantes vs não fumantes e sexo |
| **Kruskal-Wallis** | Comparação múltiplos grupos | Testar diferenças por regiões e faixas de idade |

Esses testes reforçaram que **as variáveis não seguem distribuição normal**, justificando o uso de métodos não paramétricos para comparação de médias e correlações.

---

## 🔍 Principais Insights da EDA

1. **Fumantes** — variável mais impactante sobre os custos; efeito significativo confirmado por Mann-Whitney U (p < 0.001).  
2. **IMC elevado (>30)** — influencia fortemente os custos, especialmente combinado com tabagismo.  
3. **Idade** — aumento progressivo nos custos, efeito estatisticamente relevante (Kruskal p < 0.01).  
4. **Região e sexo** — diferenças pouco expressivas, confirmadas pelos testes estatísticos.  
5. **Top 5% de custo** — perfil típico: fumante, IMC elevado, idade > 40 anos.

---

## 🧭 Próximos Passos

### 🔹 Extensão Analítica
1. Criar **features derivadas** (`age_group`, `bmi_cat`, interações `smoker*bmi`, `smoker*age`).  
2. Aplicar **log-transform** em `charges` para reduzir assimetria.  
3. Analisar **importância de variáveis** via abordagens interpretáveis (ex.: SHAP, LIME).

### 🔹 Modelagem Preditiva
1. Construir dois modelos distintos:
   - **Classificação:** prever **propensão de alto custo** (clientes top 5%).  
   - **Regressão:** estimar **valor esperado de custo (`charges`)** contínuo.  
2. Avaliar com métricas adequadas (ROC-AUC e RMSE, respectivamente).  
3. Implementar pipeline de preparação, treino e scoring.  

> 🔒 *Obs: O uso de bibliotecas específicas de machine learning (como scikit-learn) foi omitido nesta versão para foco na análise exploratória e no planejamento preditivo.*

### 🔹 Negócio e Aplicação
1. Criar **dashboard interativo** com filtros por `region`, `smoker`, `bmi_cat`, `age_group`.  
2. Apoiar **estratégias de prevenção e precificação diferenciada**.  
3. Utilizar resultados para políticas de mitigação de risco e recomendação personalizada.

---

## 📂 Estrutura do Projeto
```
insurance-analysis/
│
├── insurance.csv              # Base de dados original
├── insurance.ipynb            # Notebook com EDA e análises estatísticas
├── README_Insurance_Analysis.md # Documento de resumo e plano de ação
└── outputs/
    ├── figures/               # Gráficos e relatórios
    └── tables/                # Tabelas de resumo e estatísticas
```

---

## 🧰 Tecnologias
- **Linguagem:** Python 3.x  
- **Bibliotecas principais:** pandas, numpy, matplotlib, seaborn, scipy.stats  
- **Ambiente:** Jupyter Notebook  

---

## 🧠 Conclusão
A análise confirmou com **testes estatísticos robustos** que o hábito de fumar e o IMC elevado são fatores determinantes no custo de seguro.  
Os próximos passos envolvem a **implementação de modelos de classificação e regressão** para previsão de propensão e custo futuro, 
sustentando uma abordagem preditiva orientada a dados para o setor de seguros.
