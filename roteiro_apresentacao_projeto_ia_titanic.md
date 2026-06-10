# Roteiro de Apresentação - Projeto de IA Titanic

## Slide 1 - Título

Projeto de Inteligência Artificial: Predição de Sobrevivência no Titanic

## Slide 2 - Problema

O objetivo é prever se um passageiro sobreviveria ao naufrágio do Titanic com base em características históricas, como sexo, idade, classe da passagem, tarifa e familiares a bordo.

## Slide 3 - Tipo de aprendizagem

O problema é de aprendizagem supervisionada, pois o conjunto de treino possui a resposta correta (`Survived`). Também é um problema de classificação binária, com as classes `0` e `1`.

## Slide 4 - Dataset

Foram usados os arquivos oficiais do dataset Titanic:

- `train.csv`: treino e validação dos modelos.
- `test.csv`: predições finais.
- `gender_submission.csv`: exemplo do formato esperado.

## Slide 5 - Pré-processamento

Foram tratados valores ausentes em idade, tarifa e porto de embarque. As variáveis categóricas foram convertidas para números e os dados foram divididos em treino e validação.

## Slide 6 - Modelos

Modelos comparados:

- Regressão Logística
- KNN
- Random Forest
- XGBoost
- LightGBM

## Slide 7 - Métricas

As métricas usadas foram acurácia, precisão, recall e F1-score. Também foram analisadas matrizes de confusão, obrigatórias para problemas de classificação.

## Slide 8 - Resultados

Apresentar a tabela comparativa gerada no notebook `06_projeto_ia_comparativo_titanic.ipynb`.

## Slide 9 - Melhor modelo

Apresentar o modelo com melhor F1-score é explicar que essa métrica foi escolhida por equilibrar precisão e recall.

## Slide 10 - Conclusão

O projeto mostrou como diferentes algoritmos podem resolver o mesmo problema de classificação. A comparação entre métricas permite escolher o modelo mais adequado, em vez de depender apenas da acurácia.
