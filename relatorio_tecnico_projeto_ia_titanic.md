# Relatorio Tecnico - Projeto de Inteligencia Artificial

## 1. Tema

Predicao de sobrevivencia de passageiros do Titanic usando modelos de Aprendizagem de Maquina.

## 2. Objetivo

Desenvolver e comparar modelos capazes de classificar se um passageiro sobreviveria ao naufragio do Titanic com base em dados historicos.

## 3. Fundamentacao teorica

Aprendizagem de Maquina e uma area da Inteligencia Artificial que permite que algoritmos aprendam padroes a partir de dados historicos. Neste projeto, o objetivo e prever a variavel `Survived`, que indica se um passageiro sobreviveu ou nao.

O problema e de **aprendizagem supervisionada**, pois o conjunto de treino possui a resposta correta para cada passageiro. Tambem e um problema de **classificacao binaria**, porque existem apenas duas classes possiveis:

- `0`: nao sobreviveu
- `1`: sobreviveu

## 4. Dataset

Foi utilizado o dataset Titanic, disponibilizado pelo Kaggle. O projeto trabalha com os arquivos:

- `datas/train.csv`: conjunto de treino com 891 passageiros e a variavel alvo `Survived`.
- `datas/test.csv`: conjunto de teste com 418 passageiros, usado para gerar previsoes finais.
- `datas/gender_submission.csv`: arquivo de exemplo do formato de submissao.

Observacao: o escopo do professor cita "2 conjunto de dados". Neste projeto, foram considerados os dois arquivos oficiais do problema Titanic: treino e teste. Caso o professor exija dois datasets independentes, sera necessario adicionar uma segunda base alem do Titanic.

## 5. Analise inicial

As principais variaveis usadas foram:

- `Pclass`: classe da passagem.
- `Sex`: sexo do passageiro.
- `Age`: idade.
- `SibSp`: quantidade de irmaos/conjuges a bordo.
- `Parch`: quantidade de pais/filhos a bordo.
- `Fare`: tarifa paga.
- `Embarked`: porto de embarque.

O balanceamento das classes deve ser verificado no notebook consolidado. Essa etapa e importante porque classes muito desbalanceadas podem fazer a acuracia parecer boa mesmo quando o modelo nao aprende bem a classe minoritaria.

## 6. Pre-processamento

Foram aplicados os seguintes tratamentos:

- preenchimento de valores ausentes em `Age` com a mediana;
- preenchimento de valores ausentes em `Fare` com a mediana;
- preenchimento de valores ausentes em `Embarked` com a moda;
- transformacao de `Sex` em valores numericos;
- codificacao de `Embarked` com variaveis dummy;
- divisao do conjunto de treino em treino e validacao;
- padronizacao dos dados no KNN, pois o algoritmo depende de distancia.

## 7. Modelos utilizados

Foram comparados cinco algoritmos:

| Modelo | Principais hiperparametros |
| --- | --- |
| Regressao Logistica | `max_iter=1000`, `random_state=42` |
| KNN | `n_neighbors=7`, `StandardScaler` |
| Random Forest | `n_estimators=300`, `max_depth=6`, `min_samples_split=5`, `min_samples_leaf=2` |
| XGBoost | `n_estimators=300`, `max_depth=4`, `learning_rate=0.05` |
| LightGBM | `n_estimators=300`, `learning_rate=0.05`, `max_depth=4`, `num_leaves=15` |

## 8. Metricas de avaliacao

Como o problema e de classificacao, foram usadas as seguintes metricas:

- **Acuracia:** proporcao geral de acertos.
- **Precisao:** entre os passageiros previstos como sobreviventes, quantos realmente sobreviveram.
- **Recall:** entre os passageiros que realmente sobreviveram, quantos o modelo identificou.
- **F1-score:** equilibrio entre precisao e recall.

Tambem foram geradas matrizes de confusao para todos os modelos, conforme solicitado no escopo.

## 9. Resultados

Os resultados comparativos sao gerados no notebook:

`notebooks/06_projeto_ia_comparativo_titanic.ipynb`

Esse notebook apresenta:

- tabela comparativa com acuracia, precisao, recall e F1-score;
- matriz de confusao de cada modelo;
- identificacao automatica do melhor modelo pelo F1-score;
- geracao do arquivo final `submission_projeto_ia_titanic.csv`.

## 10. Conclusao

O projeto atende aos principais requisitos do escopo: analise dos dados, pre-processamento, aplicacao de diferentes algoritmos, comparacao com mais de tres metricas, matrizes de confusao e escolha do melhor modelo.

O modelo final deve ser escolhido com base na tabela comparativa. Para este problema, o F1-score e uma metrica adequada porque considera o equilibrio entre precisao e recall na previsao da classe de sobreviventes.

Como trabalhos futuros, podem ser testadas novas variaveis derivadas, como titulo do passageiro extraido do nome, tamanho da familia, informacoes da cabine e validacao cruzada.
