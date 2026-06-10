# Roteiro de Apresentacao - Projeto de IA Titanic

## Slide 1 - Titulo

Projeto de Inteligencia Artificial: Predicao de Sobrevivencia no Titanic

## Slide 2 - Problema

O objetivo e prever se um passageiro sobreviveria ao naufragio do Titanic com base em caracteristicas historicas, como sexo, idade, classe da passagem, tarifa e familiares a bordo.

## Slide 3 - Tipo de aprendizagem

O problema e de aprendizagem supervisionada, pois o conjunto de treino possui a resposta correta (`Survived`). Tambem e um problema de classificacao binaria, com as classes `0` e `1`.

## Slide 4 - Dataset

Foram usados os arquivos oficiais do dataset Titanic:

- `train.csv`: treino e validacao dos modelos.
- `test.csv`: predicoes finais.
- `gender_submission.csv`: exemplo do formato esperado.

## Slide 5 - Pre-processamento

Foram tratados valores ausentes em idade, tarifa e porto de embarque. As variaveis categoricas foram convertidas para numeros e os dados foram divididos em treino e validacao.

## Slide 6 - Modelos

Modelos comparados:

- Regressao Logistica
- KNN
- Random Forest
- XGBoost
- LightGBM

## Slide 7 - Metricas

As metricas usadas foram acuracia, precisao, recall e F1-score. Tambem foram analisadas matrizes de confusao, obrigatorias para problemas de classificacao.

## Slide 8 - Resultados

Apresentar a tabela comparativa gerada no notebook `06_projeto_ia_comparativo_titanic.ipynb`.

## Slide 9 - Melhor modelo

Apresentar o modelo com melhor F1-score e explicar que essa metrica foi escolhida por equilibrar precisao e recall.

## Slide 10 - Conclusao

O projeto mostrou como diferentes algoritmos podem resolver o mesmo problema de classificacao. A comparacao entre metricas permite escolher o modelo mais adequado, em vez de depender apenas da acuracia.
