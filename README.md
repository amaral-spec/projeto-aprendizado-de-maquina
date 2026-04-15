
# Análise Exploratória: Inadimplência em Cartões de Crédito

## O Problema Analisado
Este projeto foca na previsão de inadimplência de clientes de cartão de crédito em Taiwan. O objetivo principal é identificar padrões demográficos e comportamentais que indiquem um alto risco de atraso no pagamento da fatura no mês subsequente, permitindo a tomada de decisões preventivas de crédito.

## O Dataset Utilizado
A base de dados foi extraída do UCI Machine Learning Repository: [Default of Credit Card Clients Dataset](https://archive.ics.uci.edu/dataset/350/default+of+credit+card+clients). O dataset conta com 30.000 registros e 24 atributos contendo informações demográficas (idade, sexo, escolaridade, estado civil), histórico de pagamentos (abril a setembro de 2005) e limites de crédito.

## Integrantes do Grupo
* Gabriel do Amaral de Oliveira
* Emilly Cabuçu Lopes

## Resumo dos Principais Achados da EDA
*(Você preencherá isso após rodar todo o notebook e ler as conclusões)*
Exemplo: Identificamos que clientes com limites de crédito iniciais mais baixos tendem a ter uma taxa de inadimplência proporcionalmente maior. Além disso, o atraso no mês imediatamente anterior (PAY_1) demonstrou ser um forte preditor visual para o atraso no mês subsequente.

## Instruções Básicas para Execução
1. Certifique-se de ter o Python 3 instalado, junto com as bibliotecas: `pandas`, `matplotlib` e `seaborn`.
2. Baixe o dataset no link oficial e garanta que o arquivo `.csv` esteja dentro da pasta `data/` com o nome `default_of_credit_card_clients.csv`.
3. Abra o arquivo `analise_exploratoria.ipynb` em um ambiente Jupyter (Jupyter Notebook, JupyterLab ou VS Code).
4. Execute as células sequencialmente (ou utilize "Run All").
