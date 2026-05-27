# 💳 Detecção de Fraudes em Cartões de Crédito com Machine Learning

Este projeto tem como objetivo desenvolver um modelo de Machine Learning capaz de identificar transações fraudulentas em cartões de crédito, lidando com o desafio crítico de **dados altamente desbalanceados**.

## 📌 O Problema de Negócio
Fraudes em cartões de crédito geram bilhões em prejuízos anuais para as instituições financeiras. O grande desafio analítico não é apenas encontrar a fraude, mas fazê-lo sem bloquear transações legítimas. Um modelo que bloqueia muitos clientes honestos (Falsos Positivos) gera insatisfação, custos de atendimento e perda de receita (Churn). O objetivo deste projeto é encontrar o modelo com o melhor *trade-off* entre capturar fraudes (Recall) e manter uma boa experiência para o cliente (Precision).

## 📊 Sobre os Dados
O dataset utilizado contém transações realizadas por cartões de crédito europeus em dois dias de setembro de 2013. 
* **Total de Transações:** 284.807
* **Fraudes Confirmadas:** 492 (Apenas 0.172% do total)
* As variáveis preditivas (V1 a V28) passaram por uma transformação PCA para preservar a privacidade dos clientes. As únicas variáveis originais são `Time` (Tempo) e `Amount` (Valor da transação).

## 🛠️ Tecnologias e Técnicas Utilizadas
* **Python** (Pandas, NumPy) para manipulação de dados.
* **Scikit-Learn** para modelagem preditiva e métricas.
* **Imbalanced-Learn (SMOTE)** para oversampling da classe minoritária.
* **Matplotlib e Seaborn** para visualização de dados.
* **RobustScaler** para escalonamento de variáveis com presença de *outliers* financeiros.

## 🧠 Metodologia e Decisões Técnicas
1. **Pré-Processamento:** As variáveis `Time` e `Amount` foram escalonadas usando o `RobustScaler`, ideal para lidar com a variação extrema comum em transações financeiras.
2. **Balanceamento de Dados:** Como as fraudes representam menos de 0.2% dos dados, aplicar um modelo diretamente resultaria em overfitting na classe majoritária. Foi utilizado o **SMOTE** (Synthetic Minority Over-sampling Technique) apenas nos dados de treino para criar exemplos sintéticos de fraudes.
3. **Modelagem:** Foram testados dois modelos principais: **Regressão Logística** (como baseline) e **Random Forest**.

## 📈 Resultados e Conclusão
Durante a avaliação, identificamos um claro dilema de negócios:
* A **Regressão Logística** teve um ótimo Recall (0.92), mas uma Precision terrível (0.06), gerando um número inaceitável de Falsos Positivos (mais de 1.400 clientes legítimos bloqueados).
* O **Random Forest** obteve um Recall inicial de 0.82, mas com uma Precision de 0.88, impactando apenas 11 clientes legítimos.

**A Otimização Final:**
Para extrair o máximo de valor do Random Forest, realizamos o ajuste do **Threshold (Ponto de Corte)**. Ao reduzir a exigência de probabilidade de 50% para 30%, encontramos o "sweet spot" (ponto de equilíbrio) perfeito para o negócio:
* **Recall subiu para 0.88** (capturando mais fraudes).
* **Precision estabilizou em 0.72** (mantendo a experiência do cliente protegida).
* A Average Precision (AP) na curva PR-AUC foi de **0.87**, comprovando a robustez do modelo em um cenário desbalanceado.

---
**Autor:** Gabriel Motta Leite
