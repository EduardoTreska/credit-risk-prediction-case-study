# 🤖 Radar Preditivo de Risco de Crédito: Um Estudo de Caso de Machine Learning.

*Este projeto foi desenvolvido como parte de um programa de mentoria intensiva, demonstrando um ciclo completo de desenvolvimento de um modelo de classificação para um problema de negócio de alto impacto.*

## 1. Contexto de Negócio e o Problema

Em indústrias de serviços financeiros, como bancos, fintechs e especialmente em operações de cobrança, a inadimplência de clientes é um desafio crítico. A capacidade de prever quais clientes têm maior probabilidade de não cumprir com suas obrigações de pagamento permite uma alocação de recursos muito mais inteligente e eficiente.

**O Problema:** Como podemos, a partir de dados demográficos e do histórico financeiro de um cliente, identificar proativamente aqueles com maior risco de inadimplência no próximo mês, otimizando as estratégias de contato e cobrança?

## 2. A Solução: Um "Radar de Pagadores"

Este projeto desenvolve e compara múltiplos modelos de Machine Learning (Classificação) para criar um "score de risco de default". O objetivo não é apenas alcançar uma alta acurácia, mas otimizar a métrica de negócio mais importante para este caso: o **Recall** da classe de inadimplentes, garantindo que o menor número possível de clientes de risco passe despercebido.

## 3. Metodologia Aplicada

O projeto seguiu um fluxo de trabalho estruturado, simulando um ambiente profissional de Data Science:

* **Análise Exploratória de Dados (EDA):** Investigação profunda para entender as variáveis, identificar padrões e formular hipóteses.
* **Limpeza e Pré-processamento:** Tratamento de categorias inconsistentes e preparação dos dados para a modelagem. Uma abordagem de **imputação agrupada** foi utilizada para tratar dados faltantes de forma inteligente.
* **Modelagem Iterativa:** Desenvolvimento e comparação de três níveis de modelos:
    1.  **V1 (Baseline):** Regressão Logística.
    2.  **V2 (Ensemble):** RandomForest, com e sem ajuste de hiperparâmetros (`max_depth`).
    3.  **V3 (Gradient Boosting):** LightGBM, um modelo de alta performance.
* **Avaliação Focada em Negócio:** Análise dos modelos com base não apenas na acurácia, mas em um conjunto completo de métricas (Matriz de Confusão, Precisão, e principalmente Recall) para selecionar o modelo com maior valor estratégico.

## 4. Principais Descobertas da Análise Exploratória

A análise revelou que o **histórico de pagamentos recentes é o fator mais determinante para o risco de inadimplência futura**. Clientes com um histórico de atraso de 2 meses (`PAY_0 = 2`) apresentam uma probabilidade de inadimplência superior a 50% no mês seguinte, como mostra o gráfico abaixo.

## 5. Resultados e Comparação dos Modelos

O processo de modelagem iterativa permitiu uma melhoria substancial na métrica de negócio (Recall). A tabela abaixo resume a performance dos modelos testados:

<style>
    .dark-table {
        border-collapse: collapse; margin: 25px 0; font-size: 0.9em;
        font-family: sans-serif; min-width: 400px; box-shadow: 0 0 20px rgba(0, 0, 0, 0.25);
        color: #ffffff; 
    }
    .dark-table thead tr {
        background-color: #343a40; color: #ffffff; text-align: center;
    }
    .dark-table th, .dark-table td { padding: 12px 15px; text-align: center; }
    .dark-table tbody tr { background-color: #495057; border-bottom: 1px solid #6c757d; }
    .dark-table tbody tr:last-of-type { border-bottom: 2px solid #17a2b8; }
    .highlight-green { background-color: #28a745 !important; font-weight: bold; }
    .highlight-red { background-color: #dc3545 !important; font-weight: bold; }
</style>
<table class="dark-table">
    <thead>
        <tr>
            <th>Modelo</th>
            <th>Recall (Default)</th>
            <th>Precision (Default)</th>
            <th>F1-Score (Default)</th>
            <th>Acurácia</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>V1: Regressão Logística</td>
            <td>0.24 (24%)</td>
            <td>0.69 (69%)</td>
            <td>0.36</td>
            <td>81%</td>
        </tr>
        <tr>
            <td>V2: RandomForest (max_depth=10)</td>
            <td>0.34 (34%)</td>
            <td>0.64 (64%)</td>
            <td>0.45</td>
            <td>81%</td>
        </tr>
         <tr>
            <td>V2.1: RandomForest (seu ajuste)</td>
            <td>0.56 (56%)</td>
            <td>0.52 (52%)</td>
            <td>0.54</td>
            <td>79%</td>
        </tr>
        <tr>
            <td><b>V3: LightGBM (Campeão)</b></td>
            <td class="highlight-green">0.62 (62%)</td>
            <td class="highlight-red">0.47 (47%)</td>
            <td style="font-weight: bold;">0.54</td>
            <td>76%</td>
        </tr>
    </tbody>
</table>

O modelo campeão **V3 (LightGBM)**, apesar de ter a menor acurácia, foi o que melhor atendeu ao objetivo de negócio, alcançando um **recall de 62%**. Isso representa um **aumento de 158% na capacidade de detecção de inadimplentes** em comparação com o modelo baseline inicial.

## 6. Conclusões e Próximos Passos

Este projeto demonstra com sucesso a construção de um modelo de classificação robusto para um problema financeiro real. A solução desenvolvida permite a criação de um "score de risco" que pode ser usado para segmentar clientes e direcionar as ações de cobrança de forma mais eficiente e lucrativa.

**Próximos Passos Sugeridos:**
* **Otimização de Hiperparâmetros:** Utilizar técnicas como `GridSearchCV` ou `RandomizedSearchCV` para encontrar a combinação ótima de parâmetros para o LightGBM.
* **Engenharia de Features:** Criar novas variáveis a partir das existentes (ex: a razão entre o valor pago e o valor da fatura) para potencialmente aumentar a performance do modelo.
* **Deployment:** Encapsular o modelo treinado em uma API (usando Flask ou FastAPI) para que ele possa ser consumido por outros sistemas em tempo real.

## 7. Tecnologias Utilizadas
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-2C2D72?style=for-the-badge&logo=pandas&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-013243?style=for-the-badge&logo=numpy&logoColor=white)
![Seaborn](https://img.shields.io/badge/Seaborn-3776AB?style=for-the-badge&logo=seaborn&logoColor=white)
![Scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white)
![LightGBM](https://img.shields.io/badge/LightGBM-4B0082?style=for-the-badge&logo=lightgbm&logoColor=white)

![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=for-the-badge&logo=Jupyter&logoColor=white)
