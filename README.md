# Econometria.MQO
Replicando um modelo econométrico em Python para a análise de discriminação racial no mercado de trabalho dos EUA

Referência:

Título: Condições do mercado de trabalho e discriminação: existe uma ligação?
Ano: 2019

Autores: Karl David Boulware (Wesleyan University) Kenneth N. Kuttner (Williams College)

Revista: American Economic Journal

Motivação:

Este artigo analisa a discriminação no emprego com base na raça e como ela depende das condições do mercado de trabalho.

Foi usado o método dos Mínimos Quadrados Ordinários para estimar o seguinte modelo:

Yi=k+β1∗Xi+β2∗Lni+β3∗Lli+β4∗Ubi+β5∗Uni+ β6∗Uli+β7∗Di+εi

Onde i representa os 36 estados norte-americanos selecionados; Yi são as acusações de discriminação com base na raça dividido pela força de trabalho; K é o intercepto; Xi é a parcela da força de trabalho envolvidas em ocupações de “colarinho azul”; Lni e Lli são a participação de negros e latinos na força de trabalho, respectivamente; Ubi, Uni e Uli são as taxas de desemprego para brancos, negros e latinos, respectivamente; Di é uma variável dummy utilizada para discriminar os estados confederados, considerados historicamente mais racistas pela herança escravocrata e; εi é o termo de erro.

o Código usado foi

import pandas as pd
import statsmodels.formula.api as smf
import matplotlib.pyplot as plt
import statsmodels.api as sm
dados=pd.read_excel(r"C:\Users\Luiz\Documents\EUA2017.xlsx")
formula = "Yi~Xi+Ubi+Uni+Uli+Lni+Lli+Di"
model = smf.ols(formula, dados)
result = model.fit(cov_type='HC1')
print(result.summary())
fig = plt.figure()
fig = sm.graphics.plot_partregress_grid(result, fig=fig)

Os resultados enoncrados estão no quadro da regressão
![image](https://github.com/Luiz-Fernando-Oliveira/Econometria.MQO/assets/156798656/114f02ea-6236-475a-9de3-2e8454172f10)


e nos gráficos abaixo

![image](https://github.com/Luiz-Fernando-Oliveira/Econometria.MQO/assets/156798656/04987238-43c7-455e-b7b7-f4c844a27e89)

Conclusões

Em primeiro lugar, constatou-se certa dificuldade em encontrar pesquisas recentes em revistas de renome que façam análises em corte transversal. Este artigo chamou atenção por utilizar essa análise junto ao OLS (a técnica mais simples e tradicional de econometria) e ainda ser publicado no American Economic Journal.

Os resultados convergem com o trabalho original para os parâmetros de desemprego, que são insignificantes estatisticamente em todos os casos.

Os resultados divergem para os coeficientes de participação na força de trabalho por raça e para a proporção de trabalhodores de colarinho azul na força de trabalho, que foram significativos no trablho original e insignificante no presente trabalho.

O único parâmetro estatisticamente significante foi exatamente aquele não associado a teoria econômica, a dummy para estados confederados.
Os resultados 
