# Classificação e Interpretabilidade com Regressão Logística

1. Visão Geral do Projeto
Este projeto foca na aplicação do modelo de Regressão Logística (Logistic Regression) para classificar o Credit Score (variável alvo multi-classe: Low, Average, High).

Após a utilização do Naive Bayes (Módulo 20) como baseline, a Regressão Logística é introduzida como um modelo mais robusto e, crucialmente, altamente interpretável. O principal objetivo é não apenas classificar com precisão, mas também entender o peso e a direção do impacto de cada fator (ex: renda, idade, educacao) na probabilidade de um cliente pertencer a uma determinada classe de Score.

2. Pipeline de Preparação de Dados (Pré-requisitos)
O código garante que o dataset seja submetido ao mesmo pipeline de pré-processamento, essencial para a Regressão Logística.

Codificação e Limpeza: Tratamento de features categóricas e conversão de colunas como income (renda) para o tipo numérico.

Divisão de Bases: Separação em Treino e Teste (70/30).

Balanceamento (SMOTE): O SMOTE é aplicado à base de treino para equalizar as classes do Credit Score, garantindo que o modelo não seja enviesado pela classe majoritária (High).

Feature Scaling (StandardScaler): O StandardScaler é aplicado.

Justificativa: Diferente do Naive Bayes, a Regressão Logística (um modelo linear baseado em otimização por gradiente) é sensível à escala dos dados. O scaling garante que features com grandes magnitudes (ex: Renda) não dominem o cálculo dos coeficientes, sendo um passo obrigatório para este modelo.

. Modelagem: Regressão Logística Multi-classe
Algoritmo Escolhido: LogisticRegression da sklearn.

Método: Por se tratar de uma classificação com mais de duas classes (Low, Average, High), o modelo aplica automaticamente a técnica One-vs-Rest (OvR) ou Multi-nominal para estender a regressão binária ao problema multi-classe.

Treinamento: O modelo (model_lr) é treinado nas bases balanceadas e escaladas.

4. Avaliação do Desempenho
As métricas de avaliação são usadas para verificar a performance do modelo na base de teste (não vista e não balanceada).

Matriz de Confusão: Visualiza o desempenho por classe.

Relatório de Classificação: Fornece as métricas de Precision, Recall e F1-Score para cada classe individualmente. O foco aqui é verificar se a Regressão Logística, ao contrário do Naive Bayes, consegue manter um desempenho mais estável e alto nas classes minoritárias (Low e Average), que representam maior risco de crédito.

5. Interpretação dos Coeficientes
Esta é a seção mais importante, pois o modelo de Regressão Logística permite a leitura direta do impacto de cada feature.

Estrutura da Interpretação: O código extrai os coeficientes (model_lr.coef_) e os nomes das features para criar um DataFrame de fácil leitura.

Análise dos Coeficientes: Cada coeficiente representa o log-odds (logaritmo da chance) de pertencer a uma classe específica (ex: a chance de ser 'High' versus 'Low' ou 'Average').

Coeficiente Positivo: Indica que, à medida que o valor da feature aumenta (ex: a renda aumenta), a probabilidade de pertencer à classe de referência também aumenta.

Coeficiente Negativo: Indica que, à medida que o valor da feature aumenta, a probabilidade de pertencer à classe de referência diminui.

Exemplo Prático (Típico):

Um coeficiente positivo alto na feature income (renda) para a classe High de Score indica que renda mais alta está fortemente correlacionada com uma maior probabilidade de ter um Score Alto.

Um coeficiente negativo na feature debt_to_income (Dívida sobre Renda) para a classe High indica que maior endividamento está associado a uma menor probabilidade de ter Score Alto.

6. Conclusão Final e Justificativa da Escolha
A Regressão Logística é uma das melhores escolhas para a classificação de Credit Score:

Alta Interpretabilidade: Os coeficientes fornecem insights de negócio acionáveis e transparentes, explicando quais fatores e com qual peso influenciam o Score. Esta transparência é exigida em regulamentações financeiras.

Saída Probabilística: O modelo fornece uma probabilidade (e não apenas uma classificação binária dura) de pertencer a cada classe. Isso permite que a instituição financeira defina um limite de risco mais flexível e sofisticado (ex: "só aprovar se a probabilidade de Score High for superior a 80%").

Desempenho Estável: Após o balanceamento e scaling, a Regressão Logística oferece um bom equilíbrio entre acurácia e, crucialmente, a capacidade de identificar corretamente as classes de alto e baixo risco, superando as limitações do Naive Bayes.
