# 🧬 Breast Cancer Risk Analysis & Monitoring

![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)
![Grafana](https://img.shields.io/badge/grafana-%23F46800.svg?style=for-the-badge&logo=grafana&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-%23F7931E.svg?style=for-the-badge&logo=scikit-learn&logoColor=white)
![Postgres](https://img.shields.io/badge/postgres-%23316192.svg?style=for-the-badge&logo=postgresql&logoColor=white)

Este projeto une **Machine Learning** e **Business Intelligence** para transformar dados diagnósticos de cancro da mama em decisões clínicas acionáveis. O diferencial reside na capacidade de simular cenários de risco em tempo real, equilibrando a precisão do modelo com a segurança do paciente.

🎯 **Objetivo:** Otimizar a deteção precoce através da análise de *trade-offs* entre Falsos Positivos e Falsos Negativos, utilizando um Threshold Clínico ajustável.

---

## 📊 O Dashboard de Monitorização
O coração deste projeto é o dashboard interativo no **Grafana**, que consome dados processados em **PostgreSQL**.

> <img width="1440" height="413" alt="Captura de Tela 2026-03-24 às 00 26 06" src="https://github.com/user-attachments/assets/9fbb0700-0f05-470d-bb5f-2b2cf387304c" />
> <img width="1440" height="500" alt="Captura de Tela 2026-03-24 às 00 26 26" src="https://github.com/user-attachments/assets/2ca77880-1d0c-4e93-9802-fb62c8bf0056" />



*Legenda: Dashboard clínico mostrando Sensibilidade, Precisão e Matriz de Confusão Dinâmica.*

### 🎛️ Diferencial: Filtro de Threshold Interativo
Ao contrário de modelos estáticos, este dashboard permite que o utilizador escolha o limite de corte (**0.1, 0.2, 0.3, 0.5, 0.8**):
*   **Threshold 0.2 (Conservador):** Prioriza a **Sensibilidade (92%)**, garantindo que quase nenhum caso maligno é ignorado, à custa de mais alarmes falsos.
*   **Threshold 0.8 (Rigoroso):** Prioriza a **Precisão**, ideal para confirmações finais antes de procedimentos invasivos.

---

## 🛠️ Pipeline Técnica

### 1. Data Science (Python & Scikit-Learn)
*   **EDA Profunda:** Identificação de sobreposição em características como `radius_mean` através de Histogramas e Boxplots.
*   **Modelagem:** Implementação de **Regressão Logística** para obter probabilidades contínuas (0 a 1) em vez de classes fixas.
*   **Exportação:** Sincronização dos resultados (`probability`, `prediction`, `diagnosis`) com uma base de dados SQL para consumo no Grafana.

### 2. Engenharia de Dados & BI (SQL & Grafana)
*   **Consultas Dinâmicas:** SQL avançado com `CASE WHEN` e `FILTER` para gerar métricas de performance em tempo real.
*   **Métricas Críticas:**
    *   **Recall (Sensitivity):** A métrica de ouro para a segurança do paciente.
    *   **Precision:** Mede a fiabilidade dos alertas de "Risco Alto".
    *   **Confusion Matrix:** Tabela colorida para identificação imediata de erros críticos.

---

## 📈 Estrutura dos Painéis


| Painel | Tipo | Insight Clínico |
| :--- | :--- | :--- |
| **Model Sensitivity** | Gauge | Quantos % dos doentes reais o modelo detetou. |
| **Prediction Precision** | Gauge | Fiabilidade do alerta: dos casos marcados como risco, quantos são cancro. |
| **Model Confidence** | Histogram | Distribuição de probabilidades; identifica a "zona de incerteza" do modelo. |
| **Confusion Matrix** | Table | Matriz dinâmica que destaca erros críticos (Falsos Negativos) em Vermelho. |
| **Clinical Workload** | Bar Gauge | Mostra quantos pacientes entram na lista de prioridade conforme o Threshold. |
| **Radius vs Diagnosis** | Histogram | Analisa a distribuição física (raio do tumor) correlacionada ao diagnóstico. |
| **General Diagnosis** | Bar Chart | Visão geral da base de dados, comparando volume de Benignos vs Malignos. |

### 🎛️ Variável Global: Clinical Threshold
O dashboard utiliza uma variável dinâmica `${threshold}` que permite ao utilizador simular o impacto de diferentes níveis de probabilidade (**0.1 a 0.8**) em todos os painéis acima em tempo real.

---

## 🚀 Como Reproduzir este Projeto

1. **Notebook:** Execute o ficheiro `data_analysis.ipynb` para treinar o modelo e gerar o CSV/SQL.
2. **Database:** Importe os dados para o seu PostgreSQL/SQLite.
3. **Grafana:**
   * Importe o ficheiro JSON localizado em `/grafana/dashboard.json`.
   * Configure a variável `${threshold}` como tipo `Custom` com os valores `0.1, 0.2, 0.3, 0.5, 0.8`.

---

## 💻 Tecnologias
*   **Linguagem:** Python 3.x
*   **IA:** Scikit-Learn (Logistic Regression)
*   **BI:** Grafana
*   **Base de Dados:** PostgreSQL / SQLite
*   **Visualização:** Seaborn, Matplotlib

---
⭐ **Gostou desta abordagem?** Sinta-se à vontade para contribuir ou deixar uma estrela no repositório!
