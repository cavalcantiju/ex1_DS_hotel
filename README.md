#  Regressão Linear para Previsão de Preço de Hotéis

Este projeto foi desenvolvido durante um curso da **Alura** com o objetivo de aplicar **regressão linear** para prever o preço da diária de hotéis a partir de algumas características do hotel.

O projeto explora análise de dados, visualização e modelagem estatística utilizando Python.



#  Dataset

O dataset `hoteis.csv` contém informações sobre hotéis e seus preços.

## Variáveis

| Variável | Descrição |
|--------|--------|
| Estrelas | Número de estrelas do hotel |
| ProximidadeTurismo | Distância de pontos turísticos |
| Capacidade | Capacidade de hóspedes |
| Preco | Preço da diária do hotel |


#  Análise Exploratória

Primeiro foi feita uma análise de correlação entre as variáveis para entender quais características possuem maior relação com o preço.

```python
corr = dados.corr()
corr['Preco']
```

Resultado:

| Variável | Correlação com Preço |
|--------|--------|
| Estrelas | 0.40 |
| ProximidadeTurismo | -0.69 |
| Capacidade | 0.53 |

### Interpretação

- Mais estrelas → preço maior
- Mais distante do turismo → preço menor
- Maior capacidade → preço maior



#  Visualização de Dados

Foi criado um gráfico de dispersão para observar a relação entre proximidade de pontos turísticos e preço.

```python
plt.scatter(x=dados['ProximidadeTurismo'], y=dados['Preco'])
```

Também foi traçada uma reta manual para entender visualmente o conceito de regressão.

Depois utilizamos Plotly para gerar automaticamente a linha de regressão:

```python
px.scatter(dados, x="ProximidadeTurismo", y="Preco", trendline='ols')
```

---

# 🔬 Pairplot das Variáveis

Para visualizar a relação entre as variáveis e o preço:

```python
sns.pairplot(dados, y_vars='Preco', x_vars=['Estrelas', 'ProximidadeTurismo', 'Capacidade'])
```

Isso ajuda a identificar padrões e possíveis relações lineares.

---

#  Preparação dos Dados

Os dados foram separados em treino e teste usando train_test_split.

```python
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(
    x, y, test_size=0.2, random_state=42
)
```

- 80% dos dados → treino  
- 20% dos dados → teste

---

#  Modelo de Regressão Linear (OLS)

O modelo foi criado usando Statsmodels com regressão linear por Ordinary Least Squares (OLS).

```python
modelo_0 = ols(
    'Preco ~ Estrelas + ProximidadeTurismo + Capacidade',
    data=df_train
).fit()
```

### Resultado do Modelo

R² = 0.92

Isso significa que **92% da variação do preço pode ser explicada pelas variáveis do modelo**.

### Coeficientes

| Variável | Coeficiente |
|--------|--------|
| Intercept | 192.82 |
| Estrelas | +50.41 |
| ProximidadeTurismo | -19.91 |
| Capacidade | +80.94 |

### Interpretação

- Cada estrela extra aumenta o preço em aproximadamente 50
- Cada unidade de distância do turismo reduz o preço em aproximadamente 19
- Cada aumento de capacidade aumenta o preço em aproximadamente 80



#  Comparação entre Modelos

Também foram testados modelos com menos variáveis para comparar o desempenho.

| Modelo | Variáveis | R² |
|------|------|------|
| Modelo 0 | Estrelas + ProximidadeTurismo + Capacidade | 0.92 |
| Modelo 1 | Estrelas | 0.17 |
| Modelo 2 | ProximidadeTurismo | 0.49 |
| Modelo 3 | Capacidade | 0.27 |
| Modelo 4 | ProximidadeTurismo + Capacidade | 0.75 |

### Conclusão

O modelo com **todas as variáveis** apresentou o melhor desempenho.



#  Tecnologias Utilizadas

- Python  
- Pandas  
- Matplotlib  
- Seaborn  
- Plotly  
- Scikit-learn  
- Statsmodels  



# 📚 Conceitos Aplicados

- Análise exploratória de dados
- Correlação
- Visualização de dados
- Regressão linear
- OLS (Ordinary Least Squares)
- Split treino/teste
- Métrica R²



#  Conclusão

O modelo de regressão linear foi capaz de explicar grande parte da variação no preço dos hotéis.

As variáveis **estrelas, proximidade de pontos turísticos e capacidade** mostraram forte impacto no valor da diária.



# 🎓 Projeto desenvolvido durante

Curso de **Machine Learning / Regressão Linear — Alura**
