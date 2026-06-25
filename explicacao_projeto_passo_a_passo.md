# Explicação do Projeto — Passo a Passo

## O que o projeto faz?

O projeto treina e compara cinco modelos de Machine Learning para prever se um passageiro do Titanic sobreviveu ou não. Cada notebook (01 a 05) testa um modelo individualmente. O notebook 06 é o principal: ele reúne tudo, compara os modelos e gera o resultado final.

---

## Notebook 01 — Regressão Logística

**Arquivo:** `notebooks/01_titanic_logistic_regression.ipynb`

### O que acontece aqui?

**Passo 1 — Carregamento dos dados**
O notebook lê dois arquivos CSV:
- `train.csv` (891 passageiros, com a coluna `Survived` — usada para treinar)
- `test.csv` (418 passageiros, sem `Survived` — usados para gerar previsões)

**Passo 2 — Análise inicial**
Verifica quantos valores estão faltando em cada coluna. Resultado: `Age` tem 177 vazios e `Embarked` tem 2 vazios.

**Passo 3 — Pré-processamento**
Antes de treinar, os dados precisam ser limpos e transformados:
- Idade vazia → preenche com a mediana (28 anos)
- Porto vazio → preenche com a moda (S = Southampton)
- `Sex` e `Embarked` são texto → convertidos para números (0/1)
- Os 891 passageiros são divididos em **712 para treino** e **179 para validação**

**Passo 4 — Treinamento**
A Regressão Logística aprende a calcular a probabilidade de sobrevivência com base nas variáveis. Pensa em uma equação matemática que combina todas as variáveis e retorna: "probabilidade de sobreviver = X%".

**Passo 5 — Avaliação**
O modelo prevê os 179 passageiros de validação e compara com o resultado real:
- Acurácia: **80,45%**
- Melhor na classe 0 (não sobreviveu) do que na classe 1

**Passo 6 — Interpretação**
A Regressão Logística permite ver os coeficientes de cada variável. O maior impacto negativo na sobrevivência é `Sex_male` (ser homem), o que faz sentido historicamente ("mulheres e crianças primeiro").

**Passo 7 — Geração do arquivo de saída**
Gera `submission_logistic_regression.csv` com as previsões para os 418 passageiros do test.csv.

---

## Notebook 02 — KNN (K-Nearest Neighbors)

**Arquivo:** `notebooks/02_titanic_knn.ipynb`

### O que acontece aqui?

Os passos de carregamento, análise e pré-processamento são idênticos ao notebook 01. A diferença está no modelo.

**Como o KNN funciona?**
O KNN não cria uma equação. Ele simplesmente olha os K passageiros mais parecidos (vizinhos) e vota: se a maioria dos 7 vizinhos mais próximos sobreviveu, ele prevê que esse passageiro também sobreviveu.

**Passo especial — Escalonamento (StandardScaler)**
O KNN mede distância entre pontos. Se uma variável vai de 0 a 500 (Fare) e outra vai de 1 a 3 (Pclass), a distância será dominada pela variável maior. Por isso, antes de treinar, todas as variáveis são colocadas na mesma escala (média 0, desvio padrão 1).

**Resultado:**
- Acurácia: **82,12%** — melhor que a Regressão Logística

**Teste extra**
O notebook testa vários valores de K (3, 5, 7, 9, 11, 13, 15) para encontrar o melhor. O K=7 foi o escolhido.

---

## Notebook 03 — Random Forest

**Arquivo:** `notebooks/03_titanic_random_forest.ipynb`

### O que acontece aqui?

**Como o Random Forest funciona?**
Em vez de uma única árvore de decisão (que tende a decorar os dados de treino), o Random Forest cria 300 árvores diferentes. Cada árvore vota em uma resposta, e a resposta mais votada vence. Esse processo de "combinação de muitos modelos fracos" chama-se ensemble.

**Hiperparâmetros usados:**
- `n_estimators=300` → cria 300 árvores
- `max_depth=6` → cada árvore tem no máximo 6 níveis (evita overfitting)
- `min_samples_split=5` → só divide um nó se tiver pelo menos 5 exemplos
- `min_samples_leaf=2` → cada folha precisa ter pelo menos 2 exemplos

**Resultado:**
- Acurácia: **79,89%**

**Gráfico extra — Importância das variáveis**
O Random Forest calcula quais variáveis mais influenciaram as previsões:
1. `Sex_male` (42%) — ser homem reduzia muito a chance de sobreviver
2. `Fare` (19%) — tarifa paga relacionada à classe social
3. `Pclass` (13%) — classe da passagem

---

## Notebook 04 — XGBoost

**Arquivo:** `notebooks/04_titanic_xgboost.ipynb`

### O que acontece aqui?

**Como o XGBoost funciona?**
XGBoost (Extreme Gradient Boosting) é um modelo de boosting: ele treina 300 árvores em sequência, onde cada árvore nova tenta corrigir os erros da anterior. Isso o torna muito poderoso para dados tabulares.

**Hiperparâmetros:**
- `n_estimators=300` → 300 árvores em sequência
- `max_depth=4` → árvores mais rasas do que o Random Forest
- `learning_rate=0.05` → cada árvore contribui com pouco peso (aprendizado mais cuidadoso)
- `subsample=0.9` → cada árvore usa 90% dos dados aleatoriamente

**Resultado:**
- Acurácia: **79,89%**

**Importância das variáveis:**
Igual ao Random Forest: `Sex_male` (49%) domina, seguido de `Pclass` (20%).

---

## Notebook 05 — LightGBM

**Arquivo:** `notebooks/05_titanic_lightgbm.ipynb`

### O que acontece aqui?

**Como o LightGBM funciona?**
LightGBM (Light Gradient Boosting Machine) é similar ao XGBoost mas otimizado para ser mais rápido. Em vez de crescer as árvores nível por nível, ele cresce folha por folha, o que o torna mais eficiente em datasets grandes.

**Hiperparâmetros:**
- `n_estimators=300`
- `learning_rate=0.05`
- `max_depth=4`
- `num_leaves=15` → controla a complexidade da árvore (específico do LightGBM)

**Resultado:** semelhante ao XGBoost.

---

## Notebook 06 — Comparativo Final (entrega principal)

**Arquivo:** `notebooks/06_projeto_ia_comparativo_titanic.ipynb`

Este é o notebook de entrega. Ele reproduz todo o pipeline e compara todos os 5 modelos em uma única execução.

### Estrutura completa:

**Seção 1 — Fundamentação teórica**
Explica que o problema é de aprendizagem supervisionada e classificação binária. A variável `Survived` (0 ou 1) já é conhecida no treino, então o modelo aprende com exemplos rotulados.

**Seção 2 — Metodologia e análise do dataset**
Descreve os três arquivos usados (train, test, gender_submission) e as 7 variáveis selecionadas. Também apresenta uma tabela explicando cada variável.

**Análise de balanceamento**
O dataset tem 549 passageiros que não sobreviveram (61,62%) e 342 que sobreviveram (38,38%). Esse desbalanceamento é moderado e não exige técnicas como SMOTE. Por isso, além da acurácia, foram usadas Precisão, Recall e F1-score.

**Seção 3 — Pré-processamento**
O notebook define uma função `preprocess()` que aplica os mesmos tratamentos a qualquer dataset (treino ou teste), garantindo consistência. Resultado: 712 linhas para treino, 179 para validação.

**Seção 4 — Tabela de hiperparâmetros**
Documenta todos os hiperparâmetros dos 5 modelos em um único DataFrame, conforme exigido pelo escopo.

**Seção 5 — Treinamento e avaliação**
Todos os 5 modelos são treinados em sequência. Para cada um, são calculadas:

| Métrica | O que mede |
|---|---|
| Acurácia (Treino) | % de acertos nos dados de treino — detecta overfitting |
| Acurácia (Teste) | % de acertos na validação — desempenho real |
| Precisão | Dos previstos como sobreviventes, quantos realmente sobreviveram |
| Recall | Dos sobreviventes reais, quantos o modelo pegou |
| F1-score | Equilíbrio entre Precisão e Recall |

O melhor modelo é identificado automaticamente pelo F1-score.

**Seção 6 — Matrizes de confusão**
Para o melhor modelo, são plotadas duas matrizes:
- Azul: matriz no conjunto de treino
- Verde: matriz no conjunto de validação (teste interno)

A matriz de confusão mostra 4 valores:
- **Verdadeiro Negativo (canto superior esquerdo):** previu 0 e era 0 — acertou
- **Falso Positivo (canto superior direito):** previu 1 mas era 0 — errou
- **Falso Negativo (canto inferior esquerdo):** previu 0 mas era 1 — errou
- **Verdadeiro Positivo (canto inferior direito):** previu 1 e era 1 — acertou

**Seção 7 — Geração da predição final**
O melhor modelo gera as previsões para os 418 passageiros do `test.csv` e salva o arquivo `submission_projeto_ia_titanic.csv`.

**Seção 8 — Conclusão**
- Aprendizagem Supervisionada: a variável alvo era conhecida no treino
- Classificação Binária: apenas duas classes (0 ou 1)
- O F1-score foi o critério de seleção por ser robusto ao desbalanceamento
- A diferença entre Acurácia (Treino) e Acurácia (Teste) foi analisada para verificar overfitting

---

## Resumo visual do fluxo completo

```
datas/train.csv (891 passageiros)
        │
        ▼
  Pré-processamento
  ├── Preenche Age, Fare, Embarked
  ├── Codifica Sex e Embarked (números)
  └── Divide: 712 treino / 179 validação
        │
        ▼
  Treina 5 modelos
  ├── Regressão Logística
  ├── KNN (com StandardScaler)
  ├── Random Forest
  ├── XGBoost
  └── LightGBM
        │
        ▼
  Avalia cada modelo
  └── Acurácia Treino, Acurácia Teste, Precisão, Recall, F1-score
        │
        ▼
  Seleciona melhor modelo (maior F1-score)
        │
        ▼
  Gera matrizes de confusão
        │
        ▼
  Aplica no test.csv (418 passageiros)
        │
        ▼
  submission_projeto_ia_titanic.csv
```
