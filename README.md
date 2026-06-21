# Análise de Detecção de Fraudes em Cartões de Crédito

Este projeto tem como objetivo desenvolver e avaliar modelos de Machine Learning para a detecção de fraudes em transações de cartões de crédito. A detecção de fraudes é um problema crítico na indústria financeira, e a construção de modelos robustos é essencial para minimizar perdas e proteger os consumidores. O dataset utilizado contém transações anonimizadas, onde a classe alvo indica se a transação é fraudulenta (1) ou não (0).

## Sumário Executivo

Este notebook apresenta uma análise completa de um dataset de transações de cartão de crédito, com foco na identificação de fraudes. Exploramos o dataset, realizamos pré-processamento, treinamos e avaliamos diversos modelos de classificação (Regressão Logística, Random Forest, XGBoost), e utilizamos técnicas de explicabilidade (SHAP) para entender o comportamento dos modelos. O objetivo é comparar o desempenho dos modelos e identificar o mais adequado para a detecção de fraudes, considerando o desbalanceamento inerente a este tipo de dados.

## Estrutura do Projeto

O projeto está organizado nas seguintes seções:

1.  **Importação de Bibliotecas Essenciais**: Carregamento de todas as bibliotecas Python necessárias.
2.  **Carregamento e Exploração Inicial dos Dados**: Leitura do dataset e análise preliminar.
3.  **Pré-processamento de Dados**: Engenharia de features (`Amount_log`, `Amount_scaled`, `Time_scaled`) e padronização.
4.  **Treinamento e Avaliação do Modelo de Regressão Logística**: Divisão dos dados, treinamento do modelo e avaliação inicial.
5.  **Curvas ROC e Precision-Recall**: Avaliação visual e métrica de desempenho em datasets desbalanceados.
6.  **Técnicas de Balanceamento de Dados e Modelos Adicionais**: Implementação de undersampling/oversampling (SMOTE) e treinamento de Random Forest e XGBoost, além de um Pipeline.
7.  **Matriz de Confusão para XGBoost**: Análise detalhada dos erros e acertos do modelo XGBoost.
8.  **Análise de Importância das Variáveis com XGBoost**: Identificação das features mais influentes no modelo.
9.  **Ajuste de Hiperparâmetros com GridSearchCV para XGBoost**: Otimização do modelo XGBoost.
10. **Explicabilidade do Modelo com SHAP**: Compreensão do comportamento do modelo XGBoost em nível local e global.
11. **Análise Comparativa de Modelos**: Comparação das métricas de desempenho dos modelos treinados.
12. **Exportação de Métricas**: Salvamento dos resultados de desempenho em CSV.

## Como Executar

1.  **Ambiente**: Este notebook foi desenvolvido em um ambiente Google Colab. Certifique-se de ter acesso a uma conta Google.
2.  **Bibliotecas**: As bibliotecas necessárias são importadas na seção 1 do notebook. Certifique-se de que todas estão instaladas (normalmente já vêm pré-instaladas no Colab).
    - pandas: 2.2.2
    - numpy: 2.0.2
    - scikit-learn: 1.6.1
    - matplotlib: 3.10.0
    - imblearn: 0.14.2
    - xgboost: 3.2.0
    - shap: 0.52.0   
3.  **Dados**: O dataset é carregado diretamente de uma URL pública na seção 2. Nenhuma ação manual é necessária para baixar os dados.
4.  **Execução**: Execute as células do notebook em sequência, da primeira à última, para reproduzir a análise completa.

## Análise de Resultados Chave

-   **Desbalanceamento de Classes**: O dataset possui um alto desbalanceamento (aproximadamente 0.17% de transações fraudulentas), o que torna a detecção de fraudes um desafio e exige métricas de avaliação cuidadosas (e.g., Recall, Precision, F1-Score, ROC, PR Curve).
-   **Pré-processamento**: `Amount` e `Time` foram escalados para melhorar o desempenho dos modelos.
-   **Desempenho dos Modelos**: 
    -   A **Regressão Logística** forneceu uma linha de base sólida.
    -   O **Random Forest** demonstrou melhorias, especialmente no Recall.
    -   O **XGBoost** destacou-se como o modelo com o melhor desempenho geral, apresentando o maior F1-Score e um excelente balanço entre Precision e Recall para a classe minoritária (fraude), conforme detalhado no `metrics_df`:

| Model               | Precision | Recall | F1-Score |
|---------------------|-----------|--------|----------|
| Logistic Regression | 0.859813  | 0.621622 | 0.721569 |
| Random Forest       | 0.835821  | 0.756757 | 0.794326 |
| XGBoost             | 0.927419  | 0.777027 | 0.845588 |

-   **Explicabilidade (SHAP)**: As features mais importantes para a detecção de fraudes foram identificadas utilizando SHAP, fornecendo insights sobre como o modelo toma suas decisões. As principais features identificadas foram V4, V14, V26, V7 e Time.

## Conclusão

O modelo **XGBoost** demonstrou ser o mais eficaz na detecção de transações fraudulentas neste dataset, alcançando o melhor F1-Score e um bom equilíbrio entre precisão e recall. A análise de explicabilidade com SHAP forneceu informações valiosas sobre as características que mais influenciam as previsões do modelo.

Este projeto serve como um ponto de partida para a detecção de fraudes, e os modelos podem ser otimizados ainda mais com técnicas avançadas de balanceamento de dados, engenharia de features mais complexas e exploração de outros algoritmos de Machine Learning.
