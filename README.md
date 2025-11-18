# Análise Exploratória e Criação de Modelo de Classificação para Previsão de Sobrevivência no Titanic

Este projeto teve como objetivo realizar uma análise exploratória na famosa base de dados do Kaggle, ["Titanic - Machine Learning from Disaster"](https://www.kaggle.com/c/titanic), e desenvolver um modelo de classificação supervisionado para prever a sobrevivência dos passageiros.

Foi realizada a análise exploratória, o pré-processamento dos dados e, após a avaliação de diferentes algoritmos de classificação, optou-se pelo `XGBoost` em função de seu desempenho superior na fase de testes iniciais.

O modelo final alcançou uma **acurácia de 79.5%** e uma **AUC de 0.83** no conjunto de teste.

### Análise Exploratória de Dados (EDA)

A exploração inicial dos dados foi essencial para identificar dados faltantes e entender como eles poderiam impactar a decisão de utilizar uma variável na implementação do modelo.

A análise do desbalanceamento da classe alvo (`Survived`) foi importante para a decisão de estratificar os conjuntos de treino e teste, visando reduzir o viés do modelo.

No projeto, também foram verificados alguns padrões e distribuições das variáveis, o que ajudou a embasar a escolha pela imputação de dados em colunas como `Age`.

### Preparação dos Dados e Engenharia de Atributos

-   **Remoção de Colunas**: Optou-se pela remoção das colunas `PassengerId`, `Name`, `Ticket` e `Cabin`, pois não agregavam valor preditivo ao modelo ou possuíam uma grande quantidade de dados faltantes.
-   **Transformação de Variáveis**: As variáveis categóricas `Sex` e `Embarked` foram transformadas em formato numérico para serem utilizadas pelo modelo.
-   **Divisão dos Dados**: Os dados foram divididos em **70% para treino** e **30% para teste**. A divisão foi estratificada para manter a proporção da variável alvo nos dois conjuntos.
-   **Imputação de Dados**: Para a variável `Age`, os dados faltantes foram preenchidos utilizando a mediana calculada **apenas** no conjunto de treino. Essa estratégia foi aplicada a ambos os conjuntos (treino e teste) para evitar o vazamento de dados (*data leakage*).
-   **Normalização**: Os dados numéricos foram normalizados para otimizar a performance de algoritmos baseados em distância.

### Seleção e Treinamento do Modelo

-   **Modelo Baseline**: Foi criado um modelo de referência (`DummyClassifier`), que classifica sempre a classe majoritária, para servir como um ponto de comparação de desempenho a ser superado.
-   **Teste de Algoritmos**: O desempenho de diversos algoritmos de classificação foi avaliado com validação cruzada, incluindo `Logistic Regression`, `Decision Tree`, `KNN`, `SVM`, `RandomForest` e `XGBoost`.
-   **Métrica de Avaliação**: A métrica **AUC** (Area Under the Curve) foi priorizada na avaliação, por ser mais robusta para problemas com classes desbalanceadas.
-   **Modelo Escolhido**: O `XGBClassifier` foi selecionado como o modelo final por obter a melhor AUC média na validação cruzada: **0.873**.

### Avaliação do Modelo Final (XGBoost)

Resultados obtidos no **conjunto de teste**:

-   **Acurácia**: ~79.5%
-   **AUC**: 0.837

No conjunto de treino, o modelo alcançou **Acurácia de 92.5%** e **AUC de 0.976**, indicando um overfitting que deve ser tratado em otimizações futuras.

Foram analisadas também a matriz de confusão, a curva ROC e a importância de cada *feature* (*feature importance*) para o modelo final.

### Conclusão e Próximos Passos

O projeto atingiu seu objetivo principal: desenvolver um modelo com desempenho superior ao *baseline*, servindo como um ótimo estudo inicial de classificação.

Como próximos passos, sugere-se:

-   Buscar uma otimização do modelo através do **ajuste de hiperparâmetros** (*hyperparameter tuning*) para reduzir o overfitting e melhorar a performance.
-   Testar outros algoritmos ou técnicas de *ensemble*, como ***stacking***, para buscar um desempenho ainda melhor.
-   Realizar uma **engenharia de atributos mais avançada**, com a extração e criação de novas *features* para otimizar a capacidade preditiva do modelo.
