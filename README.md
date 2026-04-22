# Análise de Inadimplência em Cartões de Crédito (Credit Card Default)

## O Problema Analisado
A inadimplência de cartões de crédito é um risco constante para instituições financeiras, gerando impactos severos na geração de caixa e sustentabilidade do negócio. Este projeto busca identificar padrões e fatores (demográficos, financeiros e de comportamento de pagamento) associados à propensão de um cliente não pagar sua fatura no mês seguinte, visando subsidiar estratégias preventivas de concessão de crédito.

## O Dataset Utilizado
Utilizamos o **Default of Credit Card Clients Dataset**, proveniente de Taiwan em 2005.
- **Fonte:** [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/default+of+credit+card+clients)
- **Instâncias:** 30.000 clientes.
- **Atributos:** 24 variáveis explicativas (como Idade, Escolaridade, Limite, Histórico de pagamentos de 6 meses) e 1 variável alvo (`DEFAULT`).

## Integrantes do Grupo
- Gabriel Amaral - CP3025624
- Emilly Lopes - CP3025781

## Resumo dos Principais Achados (EDA)
1. **Histórico da fatura:** A princípio, o melhor fator determinante analisado para a veficação se o cliente é ou não inadimplente.
2.  **O histórico importa mais que o perfil:** Variáveis demográficas e limite de crédito mostraram fraca associação com a inadimplência, enquanto o status de pagamento do mês imediatamente anterior (`PAY_0`) foi o preditor mais forte.
3. **Multicolinearidade:** O valor faturado mês a mês (`BILL_AMT`) apresenta alta correlação cruzada, sugerindo redundância para modelos futuros.
4. **Escolaridade:** Foi notado um leve aumento proporcional na taxa de inadimplência em pessoas com ensino médio completo e superior completo, comparado àquelas com pós-graduação.

## Como executar o notebook
1. Clone este repositório: `git clone [link do repositorio]`
2. Certifique-se de ter instalado: Python 3, Pandas, Matplotlib e Seaborn. (Pode ser rodado via Anaconda ou Google Colab).
3. Abra o arquivo `notebook_analise.ipynb` em seu Jupyter Notebook ou em seu ambiente de preferência e execute as células sequencialmente (`Run All`). A base de dados é baixada diretamente da internet via script, sem necessidade de download manual.
