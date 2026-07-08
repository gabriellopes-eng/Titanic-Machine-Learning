# 🚢 Titanic — Predição de Sobrevivência com Machine Learning

> Projeto de **Inteligência Artificial** que treina e compara **5 algoritmos de Machine Learning** para prever se um passageiro do Titanic sobreviveu ao naufrágio, usando o clássico dataset do [Kaggle](https://www.kaggle.com/competitions/titanic).

![Python](https://img.shields.io/badge/Python-3.10+-3776AB?logo=python&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-ML-F7931E?logo=scikit-learn&logoColor=white)
![XGBoost](https://img.shields.io/badge/XGBoost-Boosting-006ACC)
![LightGBM](https://img.shields.io/badge/LightGBM-Boosting-9ACD32)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebooks-F37626?logo=jupyter&logoColor=white)
![Status](https://img.shields.io/badge/status-concluído-success)

---

## 🎬 Apresentação em vídeo

Assista à apresentação completa do projeto no LinkedIn — análise exploratória, treinamento e comparação dos modelos, avaliação e submissão final:

[![Apresentação em vídeo — Titanic Machine Learning](assets/thumbnail.png)](https://www.linkedin.com/posts/gabriel-lopes-de-albuquerque-658a8317b_machinelearning-datascience-titanic-ugcPost-7442208521053655042-zEcw)

> ▶️ Clique na imagem acima para assistir ao vídeo.

---

## 📌 Sobre o projeto

O objetivo é prever a variável alvo `Survived` — `0` (não sobreviveu) ou `1` (sobreviveu) — a partir de características dos passageiros como classe, sexo, idade, tarifa e porto de embarque.

- **Tipo de problema:** Aprendizagem Supervisionada
- **Tarefa:** Classificação Binária
- **Métricas:** Acurácia (treino e teste), Precisão, Recall, F1-score e Matriz de Confusão

---

## 🧠 Modelos comparados

| # | Modelo | Ideia central |
|---|--------|---------------|
| 01 | **Regressão Logística** | Calcula a probabilidade de sobrevivência com uma equação; permite interpretar coeficientes |
| 02 | **KNN** | Classifica pelo voto dos K vizinhos mais próximos (com `StandardScaler`) |
| 03 | **Random Forest** | Ensemble de 300 árvores de decisão votando em conjunto |
| 04 | **XGBoost** | Boosting sequencial onde cada árvore corrige os erros da anterior |
| 05 | **LightGBM** | Boosting otimizado que cresce as árvores folha a folha |
| 06 | **Comparativo Final** | Pipeline único que treina, avalia e seleciona o melhor modelo |

---

## 📊 Resultados (conjunto de validação — 179 passageiros)

| Modelo | Acurácia | Precisão | Recall | F1-score |
|--------|:--------:|:--------:|:------:|:--------:|
| 🥇 **KNN** | **82,12%** | 78% | 74% | **76%** |
| Regressão Logística | 80,45% | 79% | 67% | 72% |
| XGBoost | 79,89% | 78% | 67% | 72% |
| Random Forest | 79,89% | 82% | 61% | 70% |

> O melhor modelo é selecionado automaticamente pelo **F1-score**, critério mais robusto que a acurácia em cenários com leve desbalanceamento de classes (≈62% / 38%).

**Principais fatores de sobrevivência** (importância das variáveis): `Sex` (ser mulher), `Fare` e `Pclass` — coerente com o histórico "mulheres e crianças primeiro".

---

## 📁 Estrutura do repositório

```
Titanic-Machine-Learning/
├── datas/                                      # Datasets (train, test, gender_submission)
├── notebooks/
│   ├── 01_titanic_logistic_regression.ipynb
│   ├── 02_titanic_knn.ipynb
│   ├── 03_titanic_random_forest.ipynb
│   ├── 04_titanic_xgboost.ipynb
│   ├── 05_titanic_lightgbm.ipynb
│   └── 06_projeto_ia_comparativo_titanic.ipynb # ⭐ Notebook principal (entrega)
├── submission_*.csv                            # Predições de cada modelo
├── relatorio_tecnico_projeto_ia_titanic.md     # Relatório técnico completo
├── explicacao_projeto_passo_a_passo.md         # Explicação didática passo a passo
├── roteiro_apresentacao_projeto_ia_titanic.md  # Roteiro de apresentação
└── requirements.txt
```

---

## 🚀 Como executar

```bash
# 1. Clone o repositório
git clone https://github.com/gabriellopes-eng/Titanic-Machine-Learning.git
cd Titanic-Machine-Learning

# 2. (Opcional) Crie um ambiente virtual
python -m venv venv
# Windows
venv\Scripts\activate
# Linux / macOS
source venv/bin/activate

# 3. Instale as dependências
pip install -r requirements.txt

# 4. Abra os notebooks
jupyter notebook
```

Comece pelo notebook **`06_projeto_ia_comparativo_titanic.ipynb`**, que reúne todo o pipeline: pré-processamento → treinamento dos 5 modelos → avaliação → matrizes de confusão → geração da submissão final.

---

## 🔧 Pré-processamento

- Preenchimento de valores ausentes: `Age` e `Fare` com a mediana; `Embarked` com a moda
- Codificação de `Sex` (0/1) e `Embarked` (variáveis dummy)
- Divisão estratificada: **712 treino / 179 validação**
- Padronização com `StandardScaler` no KNN (algoritmo baseado em distância)

---

## 🛠️ Tecnologias

`Python` · `pandas` · `numpy` · `scikit-learn` · `XGBoost` · `LightGBM` · `Plotly` · `Jupyter`

---

## 🔮 Trabalhos futuros

- Extração de títulos dos nomes (Mr., Mrs., Miss...)
- Criação da variável "tamanho da família" (`SibSp + Parch`)
- Aproveitamento das informações da cabine
- Validação cruzada (k-fold)

---

## 👨‍💻 Autor

**Gabriel Lopes**
Universidade de Pernambuco — Campus Surubim · Disciplina de Inteligência Artificial

[![GitHub](https://img.shields.io/badge/GitHub-gabriellopes--eng-181717?logo=github&logoColor=white)](https://github.com/gabriellopes-eng)
