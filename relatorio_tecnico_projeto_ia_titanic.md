# Relatório Técnico - Projeto de Inteligência Artificial

## 1. Tema

Predição de sobrevivência de passageiros do Titanic usando modelos de Aprendizagem de Máquina.

## 2. Objetivo

Desenvolver e comparar modelos capazes de classificar se um passageiro sobreviveria ao naufrágio do Titanic com base em dados históricos.

## 3. Fundamentação teórica

Aprendizagem de Máquina é uma área da Inteligência Artificial que permite que algoritmos aprendam padrões a partir de dados históricos. Neste projeto, o objetivo é prever a variável `Survived`, que indica se um passageiro sobreviveu ou não.

O problema é de **aprendizagem supervisionada**, pois o conjunto de treino possui a resposta correta para cada passageiro. Também é um problema de **classificação binária**, porque existem apenas duas classes possíveis:

- `0`: não sobreviveu
- `1`: sobreviveu

## 4. Dataset

Foi utilizado o dataset Titanic, disponibilizado pelo Kaggle. O projeto trabalha com os arquivos:

- `datas/train.csv`: conjunto de treino com 891 passageiros e a variável alvo `Survived`.
- `datas/test.csv`: conjunto de teste com 418 passageiros, usado para gerar previsões finais.
- `datas/gender_submission.csv`: arquivo de exemplo do formato de submissão.

Observação: o escopo do professor cita "2 conjuntos de dados". Neste projeto, foram considerados os dois arquivos oficiais do problema Titanic: treino e teste. Caso o professor exija dois datasets independentes, será necessário adicionar uma segunda base além do Titanic.

## 5. Análise inicial

As principais variáveis usadas foram:

- `Pclass`: classe da passagem.
- `Sex`: sexo do passageiro.
- `Age`: idade.
- `SibSp`: quantidade de irmãos/cônjuges a bordo.
- `Parch`: quantidade de pais/filhos a bordo.
- `Fare`: tarifa paga.
- `Embarked`: porto de embarque.

O balanceamento das classes deve ser verificado no notebook consolidado. Essa etapa é importante porque classes muito desbalanceadas podem fazer a acurácia parecer boa mesmo quando o modelo não aprende bem a classe minoritária.

## 6. Pré-processamento

Foram aplicados os seguintes tratamentos:

- preenchimento de valores ausentes em `Age` com a mediana;
- preenchimento de valores ausentes em `Fare` com a mediana;
- preenchimento de valores ausentes em `Embarked` com a moda;
- transformação de `Sex` em valores numéricos;
- codificação de `Embarked` com variáveis dummy;
- divisão do conjunto de treino em treino e validação;
- padronização dos dados no KNN, pois o algoritmo depende de distância.

## 7. Modelos utilizados

Foram comparados cinco algoritmos:

| Modelo | Principais hiperparâmetros |
| --- | --- |
| Regressão Logística | `max_iter=1000`, `random_state=42` |
| KNN | `n_neighbors=7`, `StandardScaler` |
| Random Forest | `n_estimators=300`, `max_depth=6`, `min_samples_split=5`, `min_samples_leaf=2` |
| XGBoost | `n_estimators=300`, `max_depth=4`, `learning_rate=0.05` |
| LightGBM | `n_estimators=300`, `learning_rate=0.05`, `max_depth=4`, `num_leaves=15` |

## 8. Métricas de avaliação

Como o problema é de classificação, foram usadas as seguintes métricas:

- **Acurácia:** proporção geral de acertos.
- **Precisão:** entre os passageiros previstos como sobreviventes, quantos realmente sobreviveram.
- **Recall:** entre os passageiros que realmente sobreviveram, quantos o modelo identificou.
- **F1-score:** equilíbrio entre precisão e recall.

Também foram geradas matrizes de confusão para todos os modelos, conforme solicitado no escopo.

## 9. Resultados

Os resultados comparativos são gerados no notebook:

`notebooks/06_projeto_ia_comparativo_titanic.ipynb`

Esse notebook apresenta:

- tabela comparativa com acurácia, precisão, recall e F1-score;
- matriz de confusão de cada modelo;
- identificação automática do melhor modelo pelo F1-score;
- geração do arquivo final `submission_projeto_ia_titanic.csv`.

## 10. Conclusão

O projeto atende aos principais requisitos do escopo: análise dos dados, pré-processamento, aplicação de diferentes algoritmos, comparação com mais de três métricas, matrizes de confusão e escolha do melhor modelo.

O modelo final deve ser escolhido com base na tabela comparativa. Para este problema, o F1-score é uma métrica adequada porque considera o equilíbrio entre precisão e recall na previsão da classe de sobreviventes.

Como trabalhos futuros, podem ser testadas novas variáveis derivadas, como título do passageiro extraído do nome, tamanho da família, informações da cabine e validação cruzada.
