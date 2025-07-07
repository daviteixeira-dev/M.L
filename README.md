# Projeto: Listas de Aprendizado de Máquina (Mestrado)

Este repositório reúne todas as listas desenvolvidas para a disciplina de **Aprendizado de Máquina** do curso de Mestrado em Ciência da Computação. O objetivo dessas listas foi implementar algoritmos do zero, compreendendo seu funcionamento interno e aplicando-os a problemas reais e artificiais. Todas as listas foram desenvolvidas em **Python** utilizando apenas `numpy` e `matplotlib` (sem scikit-learn ou outras bibliotecas prontas).

> **Resumo geral:** As listas abordaram desde regressão linear até redução de dimensionalidade com PCA, totalizando seis listas bem desafiadoras, com foco em compreensão profunda dos algoritmos, suas limitações e aplicações.

---

## Lista 1: Regressão Linear, Polinomial e Regularização

### Modelos utilizados:

* **Regressão Linear:** OLS (Ordinary Least Squares), GD (Gradiente Descendente), SGD (Gradiente Estocástico)
* **Regressão Polinomial:** Regressão com graus de 1 a 13
* **Regularização L2:** Ridge Regression (lambda = 0.01)

### Por que esses modelos?

* O problema inicial envolvia a regressão de variáveis numéricas. A regressão linear foi ideal para o problema univariado inicial, e a regressão polinomial foi explorada para verificar a capacidade do modelo de se ajustar a relações mais complexas entre as variáveis. A regularização L2 foi adicionada para combater o **overfitting** em polinômios de alto grau.

### Resultados:

* OLS e GD produziram resultados semelhantes com bom desempenho em teste.
* O SGD foi sensível à ordem dos dados, mas apresentou desempenho competitivo.
* Na regressão polinomial, a partir do grau 6 houve overfitting claro (erro de validação/teste muito alto).
* Com regularização L2, os modelos polinomiais conseguiram manter desempenho estável até mesmo em graus mais altos, com melhor generalização.

---

## Lista 2: Classificação com KNN e Árvores de Decisão

### Modelos utilizados:

* **KNN (K-Nearest Neighbors)** com k variando entre 1 e 30
* **Árvore de Decisão** com poda e critério de impureza por índice de Gini

### Por que esses modelos?

* Essa lista abordou um problema de classificação de dígitos. O KNN foi escolhido por ser um modelo simples, direto e eficaz para problemas de classificação, enquanto a árvore de decisão foi usada por sua interpretabilidade e capacidade de lidar com dados categóricos e numéricos.

### Resultados:

* O melhor valor de k encontrado para o KNN foi k=4, com acurácia de 0.9625 no conjunto de validação.
* A árvore de decisão teve desempenho similar ao KNN com acurácia de 0.9575, mesmo utilizando um número reduzido de atributos por divisão.
* A matriz de confusão mostrou boa generalização nos dois modelos, com erros concentrados em dígitos visivelmente semelhantes (ex: 4 vs 9).
* As curvas de aprendizado ajudaram a observar que tanto o KNN quanto a árvore estavam bem ajustados, sem sinais evidentes de overfitting ou underfitting.

---

## Lista 3: Classificação com KNN e Árvores de Decisão (continuação)

### Modelos utilizados:

* **KNN (K-Nearest Neighbors)** com:
    * `k=1` e `k=5`
    * Distâncias: **Euclidiana** e **Mahalanobis**
* **Árvore de Decisão** com critérios:
    * **Gini**
    * **Entropia**

### Por que esses modelos?

* O conjunto de dados KC2, da NASA, apresenta características numéricas sobre códigos-fonte e uma saída binária (com ou sem defeito). Modelos simples como KNN e árvores de decisão são ideais para analisar a capacidade de generalização em contextos reais de engenharia de software, além de permitirem um bom controle sobre vieses e variâncias ao aplicar validação cruzada.

### Resultados (Validação Cruzada - 10 Folds):

| Modelo                 | Accuracy            | Precision           | Recall              | F1-score            |
| ---------------------- | ------------------- | ------------------- | ------------------- | ------------------- |
| KNN (k=1, Euclidiana)  | 0.7648 ± 0.1256     | 0.7951 ± 0.1551     | 0.7565 ± 0.1545     | 0.7629 ± 0.1161     |
| KNN (k=5, Euclidiana)  | **0.7728 ± 0.1246** | 0.7805 ± 0.1327     | **0.7636 ± 0.1650** | **0.7654 ± 0.1292** |
| KNN (k=1, Mahalanobis) | 0.6966 ± 0.1128     | 0.7318 ± 0.1427     | 0.6438 ± 0.1349     | 0.6766 ± 0.1139     |
| KNN (k=5, Mahalanobis) | 0.7594 ± 0.1055     | **0.8075 ± 0.1003** | 0.6858 ± 0.1354     | 0.7367 ± 0.1156     |
| Árvore (Gini)          | 0.6823 ± 0.1107     | 0.7073 ± 0.1515     | 0.6594 ± 0.1170     | 0.6736 ± 0.1031     |
| Árvore (Entropia)      | 0.6981 ± 0.0873     | 0.7271 ± 0.1280     | 0.6958 ± 0.1336     | 0.6948 ± 0.0778     |

### Comparação dos Modelos:

* Melhor **acurácia**: KNN k=5 (Euclidiana)
* Melhor **precisão**: KNN k=5 (Mahalanobis)
* Melhor **revocação**: KNN k=5 (Euclidiana)
* Melhor **F1-score**: KNN k=5 (Euclidiana)

### Resultados:

* Neste experimento, foi possível observar que o KNN com k=5 teve desempenho mais estável e equilibrado, principalmente com distância Euclidiana, superando tanto o KNN com k=1 quanto as árvores de decisão em quase todas as métricas. A distância Mahalanobis melhorou a precisão, mas sacrificou um pouco o recall. Já as árvores de decisão apresentaram performance inferior em todos os critérios, com destaque para a entropia, que gerou modelos mais estáveis que o Gini, mas ainda assim abaixo dos modelos KNN.

---

## Lista 4: Ensemble Learning (SVM e Random Forest)

### Modelos utilizados:

* **MLP (Multilayer Perceptron)** com:

    * 1 camada oculta
    * Treinamento por **minibatch SGD com momentum**
    * Ajuste de **número de neurônios** por busca em validação
    * Separação dos dados: 60% treino, 20% validação, 20% teste

### Por que esses modelos?

A MLP é um modelo de **regressão não linear** que pode aprender padrões complexos entre variáveis contínuas. Como a relação entre os componentes do concreto e sua resistência pode envolver interações e não linearidades, a MLP foi escolhida por sua capacidade de **modelar relações mais complexas do que a regressão linear simples**, com a vantagem de ajuste fino via validação e controle da capacidade por meio da quantidade de neurônios.

A classificação de fonemas é um problema **multiclasse com padrões não lineares**. A MLP foi escolhida por sua habilidade de aprender **fronteiras de decisão complexas** em problemas com múltiplas categorias, e por ser uma rede versátil para esse tipo de tarefa. Além disso, a validação de diferentes quantidades de neurônios permitiu ajustar a capacidade do modelo para evitar tanto **underfitting quanto overfitting**.

### Resultados:

#### Questão 1: Prever a resistência à compressão do concreto (em MPa), com base em 8 atributos físicos, usando MLP para regressão.

* Melhor número de neurônios na camada oculta: 40
* Curva de custo monitorada em treino e validação
* Métricas finais:

| Conjunto  | RMSE   | MAE    | MRE    |
| --------- | ------ | ------ | ------ |
| Treino    | 5.3181 | 4.1547 | 0.1652 |
| Validação | 6.3164 | 4.9233 | 0.1778 |
| Teste     | 6.5258 | 4.9986 | 0.1945 |

#### Questão 2: Classificar fonemas vocálicos britânicos (11 classes) com base em 10 atributos numéricos, usando MLP para classificação multiclasse.

* Melhor número de neurônios na camada oculta: 47
* Curva de custo (cross-entropy) e acurácia monitoradas
* Métricas finais:

| Conjunto  | Acurácia |
| --------- | -------- |
| Treino    | 54.21%   |
| Validação | 42.93%   |
| Teste     | 45.96%   |

#### Conclusão:

* Essa tarefa foi fundamental para compreender como redes neurais podem ser aplicadas à regressão não linear. O uso de curvas de custo e a visualização dos erros ajudaram a analisar o desempenho da rede e ajustar corretamente os hiperparâmetros. A rede conseguiu bons resultados preditivos, mesmo com estrutura simples e implementação própria.

* A curva de custo mostrou evolução do aprendizado, e a matriz de confusão ajudou a identificar os fonemas com maior índice de erro. Essa tarefa reforçou a importância de ajustar bem a capacidade do modelo para lidar com múltiplas classes e evitar underfitting.

---

## Lista 5: SVM e Comitê de Modelos (Random Forest)

### Modelos utilizados:

* **SVM com kernel RBF** (implementado do zero)
* **Random Forest** com:
    * Critério de impureza: **Índice de Gini**
    * Variação do número de classificadores base (n_estimators): 10 a 200 (de 10 em 10)
    * Variação da profundidade máxima (max_depth): 4, 6, 8, 10 e sem limite

### Por que esses modelos?

* O SVM foi escolhido por ser eficaz na criação de **fronteiras de decisão não lineares**, utilizando um **kernel RBF** para mapear os dados para um espaço de maior dimensionalidade. Já o Random Forest foi usado como **comitê de modelos**, explorando a variação entre árvores de decisão para obter uma classificação mais robusta e menos propensa ao overfitting.

### Resultados:

#### SVM com kernel RBF

* Melhores hiperparâmetros:

| C             | gamma      | Acurácia validação |
| ------------- | ---------- | ------------------ |
| 10            | 1.0        | **~79.5%**         |

#### Random Forest

* Melhores hiperparâmetros encontrados (grid search):

| n\_estimators | max\_depth | Acurácia validação |
| ------------- | ---------- | ------------------ |
| 170           | 6          | **82.00%**         |

### Observação pessoal:

* A execução completa do Random Forest com todas as combinações levou mais de 6 horas, devido à implementação manual sem paralelismo e ao grande número de árvores e profundidades.

#### Desempenho no conjunto de teste:

| Modelo        | Acurácia  | Precision | Recall | F1-score  |
| ------------- | --------- | --------- | ------ | --------- |
| SVM (RBF)     | 79.5%     | 79.1%     | 79.8%  | 79.4%     |
| Random Forest | **82.0%** | 82.7%     | 81.2%  | **81.9%** |

* O SVM apresentou desempenho sólido com fronteiras de decisão suaves, mas foi sensível à escolha dos hiperparâmetros `C` e `gamma`.
* O Random Forest superou o SVM em todas as métricas, principalmente na **robustez** e **estabilidade**, mesmo com menos ajustes de hiperparâmetros.
* A matriz de confusão dos dois modelos mostrou erros semelhantes, mas o Random Forest teve menor taxa de falsos positivos.

---

## Lista 6: K-Médias e PCA

### Modelos utilizados:

* **K-Médias (K-means):** Agrupamento não supervisionado
* **PCA (Análise de Componentes Principais):** Redução de dimensionalidade

### Por que esses modelos?

* Foram aplicados para exploração de dados não rotulados (K-means) e visualização de dados em espaços de menor dimensão (PCA).

### Resultados:

* **K-means** usando a distância Euclidiana teve melhor desempenho com K=15 (DB=0.5893).
* **K-means** com distância de Mahalanobis foi superior com K=12 (DB=0.5710).
* **PCA** mostrou que os dois primeiros componentes explicaram 88.09% da variância total dos dados. Os clusters foram bem separados no espaço 2D projetado.

---

## Conclusão Geral

Este projeto foi meu **primeiro contato com aprendizado de máquina**, e cada lista trouxe desafios importantes que me ajudaram a entender a teoria na prática. Implementar tudo do zero me forçou a compreender cada detalhe dos algoritmos, como:

* A relação entre **bias, variância e regularização**;
* A importância de **curvas de aprendizagem** e separação **treino/validação/teste**;

✳️ **Lista 1 (Regressão Linear e Regularização)**

* A influência do **grau polinomial** no viés e variância do modelo;
* Como a **regularização L2 (Ridge)** ajuda a controlar o overfitting em modelos com alta complexidade;
* Diferença de performance entre OLS, GD e SGD, e quando cada um é mais apropriado.
* Como o **SGD** é afetado pela ordem dos dados;

✳️ **Lista 2 (KNN e Árvores de Decisão)**

* Como **modelos baseados em instâncias (KNN)** reagem à variação de k e à escala dos dados;
* A importância da **poda em árvores** para evitar overfitting;
* Uso da **matriz de confusão** para interpretar erros específicos de classificação.

✳️ **Lista 3 (Distâncias e Critérios de Impureza)**

* Impacto da **distância de Mahalanobis** em datasets com correlação entre atributos;
* Comparação prática entre os critérios **Gini** e **Entropia** nas árvores de decisão;
* Como a **validação cruzada (10-fold)** aumenta a confiança nas métricas avaliadas.

✳️ **Lista 4 (MLP com regressão e classificação)**

* A sensibilidade do desempenho da rede neural ao número de **neurônios ocultos**;
* Importância da **função de custo** para ajustar o modelo via backpropagation;
* Visualizar as **curvas de erro/custo** para entender o processo de convergência do treinamento.

✳️ **Lista 5 (SVM e Random Forest)**

* Como o **SVM com kernel RBF** consegue criar **fronteiras não lineares** efetivas;
* O uso do **grid search** para encontrar hiperparâmetros ideais;
* O impacto do **paralelismo e otimização** na viabilidade computacional de ensembles como o Random Forest.

✳️ **Lista 6 (K-means e PCA)**

* Como o índice de **Davies-Bouldin** mede a qualidade de agrupamentos não supervisionados;
* A aplicação do **PCA** para identificar **dimensões mais relevantes** em datasets complexos;
* Como **PCA** facilita visualização, redução de dimensionalidade e pré-processamento.
* Como representar dados em **2D com boa separabilidade** mesmo quando o espaço original é de alta dimensão.

Além disso, aprendi como o desempenho dos modelos depende diretamente da escolha de hiperparâmetros, da qualidade dos dados e do uso adequado de técnicas de validação. Em algumas listas, especialmente na Lista 5, enfrentei limitações computacionais significativas, o que me levou a refletir sobre a importância da eficiência algorítmica e da escalabilidade em projetos reais.

No geral, esta disciplina foi extremamente enriquecedora. Mais do que simplesmente aplicar modelos prontos, pude entender como eles funcionam por dentro, os desafios envolvidos em cada etapa e as decisões que precisam ser tomadas para alcançar um bom resultado.

Saio dessa experiência muito mais confiante para aplicar e estudar técnicas de machine learning em contextos reais, tanto acadêmicos quanto profissionais — e sigo motivado a aprofundar meus conhecimentos em áreas como redes neurais profundas, aprendizado não supervisionado e métodos probabilísticos.

---

> Dedicado à disciplina de Aprendizado de Máquina - Mestrado em Ciência da Computação, 2025.

*Desenvolvido por [Davi Teixeira](https://github.com/daviteixeira-dev/).*
