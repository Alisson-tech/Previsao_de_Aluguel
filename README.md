# Previsao_de_Aluguel
O aplicativo desenvolvido durante a semana de bootcamp do canal no youtube stack.

https://www.youtube.com/c/Stack_tecnologias/videos


## Problema

Uma empresa aluga imóveis. devemos análisar a base de dados da empresa, e desenvolver um algoritmo capaz de prever o valor do aluguel dos imóveis.

## Transformando os dados utilizando airflow

Na pasta dags do repositório existe um script chamado data_pipeline.py, o script deve ser executado pelo airflow. Basicamente o script transforma os dados contidos em data/imoveis_prod.db, e copiá para uma nova base de dados data/imoveis_dw.db.

## Análise exploratória

nessa etapa análisamos os dados e tiramos alguns insights que podem ser visualizados em notebooks/analise.ipynb.

### insights importantes

#### variáveis com maior correlação ao valor do aluguel:

1. valor_seguro_incendio
2. num_banheiros
3. garagem
4. num_quartos

![img](https://github.com/Alisson-tech/Previsao_de_Aluguel/blob/master/img/correlacao.PNG)

#### Distribuição do valor do aluguel

- Possivéis outliers acima de 15000,00.
- A maioria dos valores estão na faixa de R$ 499 à 10.000,00.

![img](https://github.com/Alisson-tech/Previsao_de_Aluguel/blob/master/img/distribuicao_aluguel.PNG)

#### relação de aceitar animais com o valor do aluguel

- A maioria dos imóveis que aceitam animais, custam mais caros do que os que não aceitam.

![image](https://user-images.githubusercontent.com/62691446/123855179-f4c3ec80-d8f5-11eb-9f60-a0dee03b11e5.png)

#### Relação da mobilia com o valor do aluguel

- De todos os imóveis com valores maiores de aluguel, bem acima da média, são todos não mobiliados.
- O que justifica uma fraca correlação entre os atributos.

![image](https://user-images.githubusercontent.com/62691446/123854045-86325f00-d8f4-11eb-909e-753b4f33fd26.png)

Para mais informações abra o arquivo notebooks/aula3.ipynb.

## Modelos de Machine learning

### Outliers

Para verificar outliers utilizamos a sequinte técnica:

- encontramos a faixa interquartil \
FiQ = Q3 - Q1
- outlier baixo \
Q1 - (1.5 x FIQ)

- outlier alto \
Q3 + (1.5 x FiQ)

### teste de modelos de machine learning

Treinamos 4 diferentes modelos de I.A e utilizamos a métrica R2 para verificar qual é mais preciso.

- Regressão Linear (LIR)
- Decision Tree Regression (DTR)
- Random Forest (RFN)
- KNN Regressor (KNNR)


![img](https://github.com/Alisson-tech/Previsao_de_Aluguel/blob/master/img/modelos.PNG)

### Escolhendo o modelo

Como mostrado acima o melhor algoritmo testado foi o Random Forest, porém para escolher o melhor modelo utilizaremos a biblioteca pycaret.

Basicamente ele treina e testa diversos algoritmos de I.A e te retornar a lista em ordem do melhor algoritmo para o pior utilizando a métrica R2.

Com isso utilizando o próprio pycaret finalizamos nosso modelo utilizando o algoritmo  Catboost.

Para mais informações abra o arquivo notebooks/analise.ipynb.


## Data App

Utilizando o streamlit foi desenvolvido um aplicativo web que ao preencher as informações ele consome nosso modelo de I.A e realiza a previsão de quanto deve ser o valor de aluguel do imóvel.

https://share.streamlit.io/alisson-tech/previsao_de_aluguel/app.py

![img](https://github.com/Alisson-tech/Previsao_de_Aluguel/blob/master/img/data-app.PNG)
