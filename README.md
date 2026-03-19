# 🧬 Breast Cancer Risk Analysis & Monitoring

Este projeto combina **Data Science** e **Business Intelligence** para analisar dados diagnósticos de câncer de mama. O objetivo é desenvolver modelos preditivos (Regressão Logística) e monitorar o comportamento desses modelos através de um dashboard interativo no **Grafana**.

🎯 **Meta:** Melhorar a detecção precoce compreendendo os trade-offs entre falsos positivos e falsos negativos.

-----

## 🔍 Visão Geral do Projeto

O projeto utiliza o famoso dataset de diagnóstico de câncer de mama para classificar tumores como **Benignos (B)** ou **Malignos (M)**. A análise evolui de uma abordagem baseada em regras simples (thresholds manuais) para um modelo de aprendizado de máquina mais robusto.

-----

## 🛠️ Metodologia de Análise

### 1\. Limpeza e Preparação

  * Remoção de colunas irrelevantes (`id`, `Unnamed: 32`).
  * Mapeamento da variável alvo: `Benigno: 0`, `Maligno: 1`.
  * Verificação de valores nulos e duplicatas para garantir a integridade dos dados.

### 2\. Análise Exploratória (EDA)

  * **Distribuição:** Identificação do desbalanceamento de classes.
  * **Sobreposição:** Utilização de Boxplots para visualizar como características (como `radius_mean`) se sobrepõem entre os diagnósticos, demonstrando por que regras simples falham.

### 3\. Evolução do Modelo

  * **Abordagem por Regra Simples:** Classificação baseada apenas no raio médio.
  * **Score de Risco Pesado:** Combinação de variáveis (área, concavidade e pontos côncavos).
  * **Regressão Logística:** Implementação do modelo final para prever a probabilidade de malignidade.

-----

## 📈 Modelagem e Resultados

O modelo de **Regressão Logística** permitiu um ajuste fino na sensibilidade do diagnóstico:

  * **Acurácia Geral:** \~90%
  * **Recall (Sensibilidade):** Ao ajustar o threshold para **0.2**, conseguimos reduzir drasticamente os Falsos Negativos (casos malignos ignorados), o que é crítico em contextos médicos.
  * **Matriz de Confusão:** Monitoramento contínuo de erros do tipo I e tipo II.

-----

## 📊 Monitoramento com Grafana

Para tornar a análise acionável, estruturei um dashboard no Grafana conectado ao banco de dados (PostgreSQL). O objetivo é permitir que profissionais de saúde simulem cenários.

### 🧩 Estrutura do Dashboard

| Painel | Tipo | Descrição/Insight |
| :--- | :--- | :--- |
| **Distribuição de Diagnóstico** | Bar Chart | Visão geral da base de dados (B vs M). |
| **Classificação do Modelo** | Gauge/Stat | Total de pacientes em *High Risk* vs *Low Risk*. |
| **Radius vs Diagnosis** | Histogram | Visualiza a sobreposição de dados que causava falhas no modelo inicial. |
| **Distribuição de Probabilidade** | Histogram | Mostra como o modelo está separando as classes (confiança). |
| **Confusion Matrix** | Heatmap/Table | Exibição em tempo real dos erros (Falsos Positivos e Negativos). |
| **Impacto do Threshold** | Multi-stat | Painel dinâmico que mostra como a classificação muda conforme o filtro. |

### 🎛️ Filtro Dinâmico: Threshold

O dashboard conta com uma variável de painel onde o usuário pode selecionar o limite de corte (**0.3, 0.5, 0.7**):

  * Ao alterar o threshold, os painéis de **High Risk** e a **Matriz de Confusão** são atualizados automaticamente para mostrar o impacto clínico da decisão.

-----

## 💻 Tecnologias Utilizadas

  * **Python 3.x:** Linguagem principal.
  * **Pandas & Numpy:** Manipulação de dados.
  * **Scikit-Learn:** Inteligência Artificial (Logistic Regression, Metrics).
  * **Matplotlib & Seaborn:** Visualização de dados estatísticos.
  * **Grafana:** Dashboard de monitoramento e visualização de dados.
  * **SQL (SQLite/PostgreSQL):** Armazenamento dos dados processados para o dashboard.

-----

⭐ **Gostou do projeto?** Sinta-se à vontade para clonar e contribuir\!
