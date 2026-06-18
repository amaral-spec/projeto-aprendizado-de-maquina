# Análise de Inadimplência em Cartões de Crédito (Credit Card Default)

## O Problema Analisado
A inadimplência de cartões de crédito é um risco constante para instituições financeiras, gerando impactos severos na geração de caixa e sustentabilidade do negócio. Este projeto busca identificar padrões e fatores (demográficos, financeiros e de comportamento de pagamento) associados à propensão de um cliente não pagar sua fatura no mês seguinte. A previsão correta da classe positiva (inadimplente) permite à instituição adotar medidas preventivas, mitigando prejuízos operacionais onde o custo de um Falso Negativo (não prever o calote) é financeiramente mais danoso do que um Falso Positivo (alarme falso em cliente bom).

## O Dataset Utilizado
Utilizamos o **Default of Credit Card Clients Dataset**, proveniente de Taiwan.
- **Fonte:** [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/default+of+credit+card+clients)
- **Instâncias:** 30.000 clientes.
- **Atributos:** 24 variáveis explicativas (como Idade, Escolaridade, Limite, Histórico de pagamentos) e 1 variável alvo (`DEFAULT`).

## Integrantes do Grupo
- Gabriel Amaral - CP3025624
- Emilly Lopes - CP3025781

## Metodologia de Desenvolvimento

### 1. Análise Exploratória de Dados (Parte 1)
Principais achados identificados na fase inicial:
- **O histórico importa mais que o perfil:** Variáveis demográficas e limite de crédito mostraram fraca associação com a inadimplência, enquanto o status de pagamento do mês imediatamente anterior (`PAY_1`) foi o preditor comportamental mais forte.
- **Dinâmica de Faturas e Pagamentos:** O valor absoluto das faturas (`BILL_AMT`) isoladamente não dita o risco. O sinal de alerta está na relação entre a fatura e o que é pago (`PAY_AMT`), evidenciando o esgotamento financeiro de quem quita apenas o mínimo.
- **Multicolinearidade:** O valor faturado mês a mês apresenta alta correlação cruzada, sugerindo redundância para os modelos.
- **Escolaridade:** Foi notado um leve aumento proporcional na taxa de inadimplência em pessoas com ensino médio completo e superior completo, comparado àquelas com pós-graduação.

### 2. Modelagem e Avaliação (Parte 2)
Para a fase preditiva, adotou-se a estratégia experimental hold-out com divisão de 80% para treinamento e 20% para teste, utilizando estratificação (`stratify=y`) para preservar a proporção de 22% de inadimplentes da base original e evitar vazamento de dados (*data leakage*).

Tratamentos aplicados exclusivamente ao conjunto de treino:
- **Normalização:** `StandardScaler` para reajustar a escala das faturas e limites financeiros.
- **Balanceamento:** Aplicação do `SMOTE` para criar instâncias sintéticas da classe minoritária (calotes), igualando o jogo em 50/50 e impedindo o vício dos modelos na classe majoritária.

Algoritmos implementados e comparados:
1. **Regressão Logística:** Modelo baseline linear para estabelecer o piso de desempenho.
2. **Random Forest:** Ensemble baseado em árvores para capturar não-linearidades.
3. **XGBoost:** Algoritmo de boosting de alta performance para refinar a classificação tabular.

## Principais Resultados da Modelagem

Os modelos foram testados com dados reais e desbalanceados, apresentando o seguinte balanço de métricas na classe alvo (1):

| Modelo | ROC-AUC | Precisão (Classe 1) | Recall (Classe 1) | F1-Score (Classe 1) |
| :--- | :---: | :---: | :---: | :---: |
| **Regressão Logística (Baseline)** | 0.7160 | 37% | 63% | 0.47 |
| **Random Forest** | 0.7588 | 54% | 46% | 0.50 |
| **XGBoost** | 0.7496 | 58% | 41% | 0.48 |

### Conclusões de Negócio
- **Random Forest** obteve o melhor desempenho estatístico macro (ROC-AUC de 0.7588 e F1-Score de 0.50), mostrando-se o modelo ideal para equilibrar a proteção do caixa com a boa experiência do cliente.
- **Regressão Logística** atua como um alarme altamente sensível (Recall de 63%), indicado caso a prioridade do banco seja reter prejuízos a qualquer custo, assumindo o risco de gerar mais atritos por falsos alarmes.
- **XGBoost** destacou-se pela assertividade (Precisão de 58%), minimizando bloqueios indevidos em clientes adimplentes.

### Abordagem Avançada: Interpretabilidade via SHAP
Para dar transparência ao modelo de caixa-preta do XGBoost, foi utilizada a biblioteca SHAP (SHapley Additive exPlanations). O gráfico de resumo confirmou os achados da análise exploratória: o atraso no mês mais recente (`PAY_1`) foi categorizado como a variável de maior peso individual para empurrar o modelo em direção à previsão de inadimplência, enquanto limites de crédito mais altos atuaram como fatores de ancoragem para segurança.
