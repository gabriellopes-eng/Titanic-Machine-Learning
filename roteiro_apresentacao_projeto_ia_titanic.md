# Roteiro de Apresentação - Projeto de IA Titanic

## Slide 1 - Título

**Fala sugerida:**

Bom dia. O nosso trabalho tem como tema a aplicação de Aprendizagem de Máquina para prever a sobrevivência de passageiros do Titanic. O objetivo é usar dados históricos dos passageiros para treinar modelos capazes de classificar se uma pessoa sobreviveria ou não ao naufrágio.

## Slide 2 - Objetivo do projeto

**Fala sugerida:**

O objetivo principal do projeto é desenvolver modelos de Aprendizagem de Máquina capazes de realizar uma classificação com base em dados históricos. No nosso caso, a classificação é binária, porque temos apenas duas possibilidades: o passageiro não sobreviveu, representado por `0`, ou sobreviveu, representado por `1`.

Esse objetivo está de acordo com o escopo da disciplina, que pede a aplicação de modelos de Machine Learning para classificação ou predição.

## Slide 3 - Problema estudado

**Fala sugerida:**

O problema que queremos resolver é: a partir de características de um passageiro do Titanic, como classe da passagem, sexo, idade, número de familiares a bordo, tarifa paga e porto de embarque, é possível prever se ele sobreviveu?

Esse é um problema relevante para estudo porque envolve dados reais, variáveis numéricas e categóricas, valores ausentes e comparação entre diferentes algoritmos de classificação.

## Slide 4 - Tipo de aprendizagem

**Fala sugerida:**

O tipo de aprendizagem utilizado é **aprendizagem supervisionada**.

Ela é supervisionada porque o conjunto de treino já possui a resposta correta para cada passageiro. Essa resposta está na coluna `Survived`, que informa se o passageiro sobreviveu ou não.

Em outras palavras, durante o treinamento, o modelo recebe os dados de entrada, como idade, sexo e classe da passagem, e também recebe a saída correta. A partir disso, ele aprende padrões que depois são usados para prever novos casos.

Não é aprendizagem não supervisionada porque não estamos apenas agrupando passageiros sem rótulo. Também não é semi-supervisionada, porque a etapa principal do projeto usa dados rotulados.

## Slide 5 - Dataset utilizado

**Fala sugerida:**

O dataset utilizado foi o Titanic, disponibilizado pelo Kaggle. Ele é bastante usado em estudos de Machine Learning porque apresenta um problema de classificação bem definido e permite testar várias etapas importantes de um projeto de IA.

Foram usados os arquivos:

- `train.csv`, que contém os dados dos passageiros e a variável alvo `Survived`;
- `test.csv`, usado para gerar predições finais;
- `gender_submission.csv`, que serve como exemplo do formato esperado para submissão.

No projeto, a avaliação dos modelos foi feita separando uma parte do `train.csv` para validação, porque o `test.csv` oficial não possui a resposta real.

## Slide 6 - Análise inicial dos dados

**Fala sugerida:**

Na análise inicial, verificamos o tamanho da base, os tipos de variáveis, os valores ausentes e o balanceamento das classes.

O balanceamento é importante porque, se uma classe aparece muito mais que a outra, um modelo pode parecer bom apenas por prever sempre a classe majoritária. No Titanic, existem mais passageiros que não sobreviveram do que passageiros que sobreviveram, então é importante avaliar o modelo com mais de uma métrica, e não apenas com acurácia.

## Slide 7 - Pré-processamento

**Fala sugerida:**

Antes de treinar os modelos, foi necessário fazer o pré-processamento dos dados.

Primeiro, selecionamos as principais variáveis: `Pclass`, `Sex`, `Age`, `SibSp`, `Parch`, `Fare` e `Embarked`.

Depois, tratamos valores ausentes. A idade foi preenchida com a mediana, a tarifa também foi preenchida com a mediana e o porto de embarque foi preenchido com a moda.

Também transformamos variáveis categóricas em valores numéricos. A variável `Sex` foi convertida para números, e a variável `Embarked` foi transformada usando variáveis dummy.

Por fim, separamos os dados em treino e validação, mantendo a proporção das classes.

## Slide 8 - Modelos aplicados

**Fala sugerida:**

Foram aplicados diferentes algoritmos de Machine Learning, como solicitado no escopo.

Os modelos testados foram:

- Regressão Logística;
- KNN;
- Random Forest;
- XGBoost;
- LightGBM.

A Regressão Logística é um modelo simples e interpretável para classificação binária. O KNN classifica com base na proximidade entre exemplos. O Random Forest combina várias árvores de decisão. O XGBoost e o LightGBM são modelos de boosting, muito usados em problemas tabulares por apresentarem bom desempenho.

## Slide 9 - Hiperparâmetros

**Fala sugerida:**

Também foi criada uma tabela de hiperparâmetros dos modelos, conforme o escopo pede.

Por exemplo, no KNN foi definido o número de vizinhos. No Random Forest foram definidos o número de árvores, a profundidade máxima e a quantidade mínima de amostras para divisão. No XGBoost e no LightGBM foram definidos parâmetros como número de estimadores, taxa de aprendizado e profundidade.

Essa tabela é importante porque documenta as configurações usadas em cada modelo e permite entender como os resultados foram obtidos.

## Slide 10 - Métricas de avaliação

**Fala sugerida:**

Para comparar os modelos, usamos quatro métricas de avaliação:

- **Acurácia**, que mede a proporção total de acertos;
- **Precisão**, que indica, entre os passageiros previstos como sobreviventes, quantos realmente sobreviveram;
- **Recall**, que indica, entre os sobreviventes reais, quantos o modelo conseguiu identificar;
- **F1-score**, que combina precisão e recall em uma única métrica.

O escopo pede no mínimo três métricas, então usamos quatro para fazer uma avaliação mais completa.

## Slide 11 - Resultados comparativos

**Fala sugerida:**

Depois do treinamento, os modelos foram comparados em uma tabela com acurácia, precisão, recall e F1-score.

O modelo escolhido como mais adequado foi o que apresentou melhor F1-score. Escolhemos o F1-score como critério principal porque ele equilibra precisão e recall, o que é importante em problemas de classificação quando queremos avaliar bem as duas classes.

No notebook, o melhor modelo encontrado foi o KNN.

## Slide 12 - Matriz de confusão

**Fala sugerida:**

Como o problema é de classificação, o escopo exige matriz de confusão.

A matriz de confusão mostra os acertos e erros do modelo divididos por classe. Na diagonal principal ficam os acertos: passageiros que realmente não sobreviveram e foram previstos como não sobreviventes, e passageiros que realmente sobreviveram e foram previstos como sobreviventes.

Fora da diagonal ficam os erros: passageiros que foram classificados incorretamente.

No notebook, apresentamos a matriz de confusão em formato visual, separando treinamento e teste interno. Esse teste interno é a parte de validação separada do conjunto de treino, já que o `test.csv` oficial do Kaggle não possui a coluna real `Survived`.

## Slide 13 - Melhor modelo

**Fala sugerida:**

O modelo mais adequado para o problema foi escolhido com base na comparação das métricas. No resultado obtido, o KNN teve o melhor F1-score.

Isso significa que, dentro da divisão de treino e validação utilizada, ele conseguiu um bom equilíbrio entre identificar corretamente os sobreviventes e evitar classificações incorretas.

Mesmo assim, é importante lembrar que o resultado pode variar com outras divisões dos dados ou com novos ajustes de hiperparâmetros.

## Slide 14 - Conclusão

**Fala sugerida:**

Concluímos que o projeto atende ao objetivo de aplicar Aprendizagem de Máquina em um problema de classificação usando dados históricos.

Foram realizadas as etapas de análise dos dados, pré-processamento, treinamento de diferentes modelos, comparação por métricas, análise por matriz de confusão e escolha do modelo mais adequado.

O trabalho mostra que não basta treinar apenas um modelo. É importante comparar algoritmos diferentes e usar várias métricas para tomar uma decisão mais confiável.

## Slide 15 - Possíveis melhorias

**Fala sugerida:**

Como melhoria futura, poderíamos criar novas variáveis a partir dos dados originais. Por exemplo, extrair o título do passageiro a partir do nome, criar uma variável de tamanho da família ou usar informações da cabine.

Também seria possível aplicar validação cruzada e testar outros modelos ou técnicas de ajuste de hiperparâmetros.

Por fim, caso seja necessário atender de forma mais rigorosa ao item do escopo que menciona dois conjuntos de dados, poderíamos adicionar uma segunda base independente e repetir a metodologia.
