# desafio-analise-de-credito

# Desafio de Ciência de Dados – Crédito (Projetos 1 e 2)

Este repositório apresenta a solução para dois desafios de Ciência de Dados na área de crédito, envolvendo **modelos de classificação binária**, análise exploratória, pré-processamento, avaliação técnica e interpretação de impacto de negócio.

Os projetos foram desenvolvidos em Jupyter Notebooks, com foco em **clareza, reprodutibilidade e aderência a cenários reais de produção**.

---
'''
## Estrutura do Repositório

notebooks/

00_data_extraction.ipynb

01_proj1_eda_and_preprocessing.ipynb

02_proj1_modeling.ipynb

03_proj2_completo.ipynb


data/

raw/ # dados originais (não versionados)

processed/ # dados processados (não versionados)

outputs/ # artefatos finais (ex.: OOT escorada)


.gitignore

requirements.txt
'''

---

## Visão Geral dos Notebooks

### `00_data_extraction.ipynb`
Notebook responsável pela **leitura e preparação inicial das bases de dados**, utilizado como etapa comum aos dois projetos.  
Centraliza a carga das bases, padronização inicial e separação lógica por desafio.

---

## Projeto 1 – Modelo de Concessão de Crédito

### Objetivo
Desenvolver um **modelo de concessão de crédito** para classificar clientes como **Bom Pagador** ou **Mau Pagador**, além de avaliar o impacto financeiro da substituição de uma política de crédito tradicional por uma política baseada em score de machine learning.

### Dataset
- Aproximadamente **150 variáveis** (majoritariamente mascaradas)
- Chave: `ID`
- Variável alvo (`TARGET`):
  - `0` → Bom Pagador  
  - `1` → Mau Pagador (atraso > 60 dias em 2 meses)
- O **score do modelo representa a probabilidade de Bom Pagador**
- Divisão temporal:
  - **Treino**: jan–ago/2017
  - **Teste**: jan–ago/2017
  - **Out-of-Time (OOT)**: set–nov/2017 (base cega, sem TARGET)

---

### Notebooks do Projeto 1

#### `01_proj1_eda_and_preprocessing.ipynb`
- Entendimento da base e análise exploratória dos dados
- Tratamento de valores ausentes
- Codificação de variáveis categóricas
- Preparação das bases de Treino, Teste e OOT
- Garantia de consistência de features entre as bases

#### `02_proj1_modeling.ipynb`
- Treinamento de modelos de classificação binária (XGBoost)
- Ajuste de hiperparâmetros
- Avaliação técnica:
  - ROC AUC
  - Gini
  - KS
- Comparação entre modelo baseline e modelo otimizado
- **Análise financeira**:
  - Política **AS-IS**: reprovação por idade ≤ 28 anos
  - Política **TO-BE**: reprovação por score
  - Avaliação considerando agosto/2017 e empréstimos de R$1.000
- **Escoragem da base Out-of-Time**:
  - Aplicação do modelo e do cutoff definido na base de Teste
  - Estratégia de **ancoragem**, sem recalibração
  - Geração de score e decisão de crédito (sem criação de TARGET)

---

## Projeto 2 – Modelo de Recuperação de Dívidas

### Objetivo
Desenvolver um **modelo de recuperação de dívidas**, classificando clientes quanto à probabilidade de serem **Bons ou Maus Pagadores**, com foco não apenas na performance técnica, mas também na **interpretação de impacto de negócio**.

### Dataset
- Aproximadamente **203 variáveis** (majoritariamente mascaradas)
- Chave: `index`
- Variável alvo:
  - `0` → Bom Pagador  
  - `1` → Mau Pagador
- O **score representa a probabilidade de Bom Pagador**, com critérios explicitados ao longo da análise
- Dados localizados em `../datasets/credit_02`

---

### Notebook do Projeto 2

#### `03_proj2_completo.ipynb`
- Análise exploratória dos dados
- Pré-processamento e engenharia de features
- Treinamento de modelo de classificação binária
- Avaliação técnica do desempenho
- **Análise de negócio**:
  - Interpretação dos resultados
  - Discussão de como o modelo pode impactar positivamente a empresa e seus clientes
  - Recomendações baseadas nos resultados obtidos

---

## Considerações Importantes

- As bases de dados **não são versionadas** neste repositório por restrições de uso.
- A base Out-of-Time do Projeto 1 é tratada como **base cega**, sendo utilizada apenas para escoragem.
- O projeto busca simular **boas práticas de ambientes reais**, incluindo:
  - separação temporal
  - ausência de vazamento de informação
  - ancoragem de políticas de decisão
  - foco em impacto de negócio, não apenas métricas técnicas

---

## Tecnologias Utilizadas

- Python
- Pandas / NumPy
- Scikit-learn
- XGBoost
- Matplotlib / Seaborn
- Jupyter Notebook

---

## Observação Final

Este repositório foi estruturado para refletir um fluxo completo de trabalho em Ciência de Dados, desde a ingestão de dados até a interpretação de resultados para tomada de decisão, alinhado a desafios reais da área de crédito.
