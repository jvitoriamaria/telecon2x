# 📊 Relatório: Previsão de Churn – Telecom X

---

## 1. Introdução

Este relatório apresenta a análise e o desenvolvimento de modelos preditivos para identificar clientes com maior probabilidade de cancelar os serviços da Telecom X. O objetivo é antecipar a evasão para possibilitar ações preventivas eficazes.

---

## 2. Preparação dos Dados

- Dados obtidos no formato JSON, com informações dos clientes e serviços.
- Conversão da variável alvo **`Churn`** para binário (1 = cancelou, 0 = ativo).
- Remoção de registros com valores nulos e filtragem para manter somente dados válidos.
- Transformação das variáveis categóricas em variáveis dummy (one-hot encoding).

---

## 3. Análise Exploratória e Seleção de Variáveis

- Identificamos as variáveis mais relevantes para o churn:
  - **Tipo de contrato**: contratos mensais têm maior risco.
  - **Forma de pagamento**: pagamento via boleto associado a maior evasão.
  - **Tempo de contrato (tenure)**: clientes recentes saem mais.
  - **Serviços adicionais**: ausência de pacotes de suporte e segurança.
  - **Valor total gasto**: clientes com gastos baixos têm maior propensão.

---

## 4. Modelagem e Avaliação

Treinamos dois modelos de classificação:

| Modelo               | Acurácia | ROC AUC |
|----------------------|----------|---------|
| Regressão Logística  | 0.81     | 0.87    |
| Random Forest        | 0.84     | 0.91    |

O modelo **Random Forest** apresentou melhor performance e será priorizado para ações futuras.

---

## 5. Importância das Variáveis

Visualizamos as 10 variáveis mais importantes segundo o modelo Random Forest:

```python
import matplotlib.pyplot as plt
import seaborn as sns
import numpy as np

importancias = modelo_rf.feature_importances_
indices = np.argsort(importancias)[::-1]
nomes_variaveis = X.columns[indices]

plt.figure(figsize=(12, 8))
sns.barplot(x=importancias[indices][:10], y=nomes_variaveis[:10])
plt.title('Top 10 Variáveis Mais Importantes - Random Forest')
plt.tight_layout()
plt.show()

