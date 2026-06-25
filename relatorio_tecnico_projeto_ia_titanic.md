# Relatório Técnico - Projeto de Inteligência Artificial

**Instituição:** Universidade de Pernambuco — Campus Surubim  
**Disciplina:** Inteligência Artificial  
**Aluno:** Gabriel Lopes  
**Tema:** Predição de Sobrevivência no Titanic com Aprendizagem de Máquina

---

## 1. Fundamentação Teórica

### Descrição do problema

O objetivo deste projeto é prever se um passageiro do Titanic sobreviveu ao naufrágio com base em suas características pessoais, como classe da passagem, sexo, idade, número de familiares a bordo, tarifa paga e porto de embarque. A variável alvo `Survived` assume apenas dois valores — `0` (não sobreviveu) ou `1` (sobreviveu).

### Tipo de Aprendizagem

O problema é de **Aprendizagem Supervisionada**, pois o conjunto de treino já possui a resposta correta (a variável `Survived`) para cada passageiro. Os modelos aprendem a relação entre as features e o resultado a partir de exemplos rotulados e, em seguida, generalizam para novos dados não vistos.

Por possuir apenas duas classes possíveis, o problema é especificamente uma **classificação binária**.

---

## 2. Metodologia

### Escolha do Dataset

Foi utilizado o dataset **Titanic**, obtido na plataforma **Kaggle**. Os arquivos utilizados foram:

- `datas/train.csv`: conjunto de treino com **891 passageiros** e a variável alvo `Survived`.
- `datas/test.csv`: conjunto de teste com **418 passageiros**, usado para gerar as predições finais.
- `datas/gender_submission.csv`: arquivo de exemplo do formato de submissão.

### Variáveis utilizadas

| Variável | Descrição |
| --- | --- |
| `Pclass` | Classe da passagem (1ª, 2ª ou 3ª) |
| `Sex` | Sexo do passageiro |
| `Age` | Idade |
| `SibSp` | Quantidade de irmãos/cônjuges a bordo |
| `Parch` | Quantidade de pais/filhos a bordo |
| `Fare` | Tarifa paga |
| `Embarked` | Porto de embarque |

### Balanceamento das classes

O balanceamento foi verificado conforme solicitado no escopo:

| Classe | Quantidade | Percentual |
| --- | --- | --- |
| Não sobreviveu (0) | 549 | 61,62% |
| Sobreviveu (1) | 342 | 38,38% |

O dataset apresenta um leve desbalanceamento, com a classe majoritária representando cerca de 62% dos dados. Esse nível de desequilíbrio é considerado moderado e não compromete significativamente o treinamento dos modelos utilizados. Por esse motivo, optou-se por não aplicar técnicas de balanceamento artificial (como SMOTE ou `class_weight='balanced'`), priorizando a preservação da distribuição original dos dados históricos. As métricas de Precisão, Recall e F1-score foram incluídas para complementar a Acurácia e garantir uma avaliação mais robusta mesmo diante desse desequilíbrio.

### Pré-processamento

Foram aplicados os seguintes tratamentos:

- preenchimento de valores ausentes em `Age` com a mediana do treino;
- preenchimento de valores ausentes em `Fare` com a mediana do treino;
- preenchimento de valores ausentes em `Embarked` com a moda do treino;
- codificação de `Sex` para valores numéricos (0 = male, 1 = female);
- codificação de `Embarked` com variáveis dummy;
- divisão do conjunto de treino em treino (712 registros) e validação (179 registros) com estratificação pela classe alvo;
- padronização dos dados no KNN com `StandardScaler`, pois o algoritmo depende de distância.

### Tabela de hiperparâmetros dos modelos

| Modelo | Parâmetro | Valor |
| --- | --- | --- |
| Regressão Logística | max_iter | 1000 |
| Regressão Logística | random_state | 42 |
| KNN | n_neighbors | 7 |
| KNN | scaler | StandardScaler |
| Random Forest | n_estimators | 300 |
| Random Forest | max_depth | 6 |
| Random Forest | min_samples_split | 5 |
| Random Forest | min_samples_leaf | 2 |
| XGBoost | n_estimators | 300 |
| XGBoost | max_depth | 4 |
| XGBoost | learning_rate | 0,05 |
| XGBoost | subsample | 0,9 |
| LightGBM | n_estimators | 300 |
| LightGBM | learning_rate | 0,05 |
| LightGBM | max_depth | 4 |
| LightGBM | num_leaves | 15 |

---

## 3. Resultados

### Tabela comparativa dos modelos

Os resultados completos são gerados ao executar o notebook `notebooks/06_projeto_ia_comparativo_titanic.ipynb`. A tabela abaixo apresenta os valores obtidos no conjunto de validação (179 passageiros):

| Modelo | Acurácia (Treino) | Acurácia (Teste) | Precisão | Recall | F1-score |
| --- | --- | --- | --- | --- | --- |
| KNN | — | 82,12% | 78% | 74% | 76% |
| Regressão Logística | — | 80,45% | 79% | 67% | 72% |
| XGBoost | — | 79,89% | 78% | 67% | 72% |
| Random Forest | — | 79,89% | 82% | 61% | 70% |
| LightGBM | — | — | — | — | — |

> Os valores de Acurácia (Treino) e os resultados do LightGBM são preenchidos automaticamente na execução do notebook.

### Matrizes de confusão

Obrigatórias para problemas de classificação. As matrizes são geradas no notebook para o melhor modelo (selecionado pelo F1-score), nos dois conjuntos:

- **Treinamento** (azul): avalia o ajuste do modelo aos dados de treino.
- **Teste/Validação** (verde): avalia a capacidade de generalização.

Exemplo de leitura — KNN no conjunto de validação:

|  | Predito: Não sobreviveu | Predito: Sobreviveu |
| --- | --- | --- |
| **Real: Não sobreviveu** | 96 ✓ | 14 ✗ |
| **Real: Sobreviveu** | 18 ✗ | 51 ✓ |

---

## 4. Conclusão

O projeto aplicou cinco algoritmos de Machine Learning a um problema de **classificação binária supervisionada**, comparando-os com cinco métricas: Acurácia (Treino), Acurácia (Teste), Precisão, Recall e F1-score, além das matrizes de confusão obrigatórias para problemas de classificação.

O modelo com melhor desempenho foi identificado automaticamente pelo **F1-score**, critério mais robusto que a acurácia simples em cenários com desbalanceamento de classes. A diferença entre a Acurácia (Treino) e a Acurácia (Teste) foi analisada para verificar overfitting.

Como trabalhos futuros, podem ser testadas: extração de títulos dos nomes dos passageiros, criação de variável de tamanho da família, aproveitamento de informações da cabine e validação cruzada.
