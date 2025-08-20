# Telecom-X1

Análise de Evasão de Clientes na Telecom X
Com o arquivo de dados em mãos, vamos dar início ao nosso plano de análise. Primeiramente, farei o processamento dos dados para garantir que estejam prontos para a exploração. Em seguida, farei uma análise exploratória para identificar os principais fatores que levam à evasão de clientes.

1. Processamento e Limpeza dos Dados (ETL)
A primeira etapa foi extrair e carregar os dados do arquivo JSON para um DataFrame do pandas. Como o arquivo tem uma estrutura aninhada, eu a organizei em um formato de tabela plana.

Durante a inspeção dos dados, notei algumas inconsistências que precisam ser corrigidas:

A coluna TotalCharges foi importada como texto (object) e continha alguns valores em branco. Para corrigi-la, converti a coluna para um tipo numérico e preenchi os valores ausentes com a mediana da própria coluna, a fim de não perder dados.

A coluna Churn também tinha valores ausentes, representados por uma string vazia ''. Eu a preenchi com o valor 'No', assumindo que clientes sem um status de churn registrado ainda não cancelaram.

Depois do tratamento, o conjunto de dados tem as seguintes características:

Total de colunas: 20

Total de linhas: 241

Valores não-nulos: Todas as colunas possuem 241 valores, exceto TotalCharges e MonthlyCharges, que tinham valores ausentes e foram preenchidos.

Tipos de dados: As colunas foram convertidas para tipos adequados, como float64 para os valores de cobrança e int64 para o tempo de permanência (tenure).

2. Análise Exploratória de Dados (EDA) e Insights
Após a limpeza, analisei a taxa de evasão (churn rate) em relação a diferentes variáveis, buscando padrões que possam ser úteis para a equipe de Data Science.

Taxa de Evasão por Tipo de Serviço de Internet

A análise mostra uma diferença significativa na taxa de evasão com base no tipo de serviço de internet do cliente:

DSL: 13,8%

Fibra Óptica: 36,9%

Sem Serviço de Internet: 8,2%

Isso sugere que clientes que utilizam o serviço de fibra óptica têm uma probabilidade de evasão consideravelmente maior do que os de DSL. Curiosamente, a menor taxa de evasão é entre aqueles que não têm serviço de internet, o que pode indicar que esses clientes usam apenas o serviço de telefone da empresa e estão mais satisfeitos.

Taxa de Evasão por Tipo de Contrato

O tipo de contrato também parece ser um fator importante:

Mensal: 42,7%

Um ano: 13,3%

Dois anos: 3,8%

A alta taxa de evasão de clientes com contratos mensais é um indicativo forte de que a flexibilidade de cancelamento imediato pode estar ligada à insatisfação. Clientes com contratos de 1 ou 2 anos tendem a permanecer fiéis à empresa.

Tempo de Permanência (tenure) e Churn

A média de tempo de permanência é um forte preditor de churn:

Clientes que não cancelaram (Churn=0): 39.88 meses

Clientes que cancelaram (Churn=1): 17.51 meses

A diferença é notável. Clientes que evadiram tinham, em média, uma permanência significativamente menor do que os que permaneceram na empresa. Isso reforça a ideia de que a insatisfação leva a um cancelamento mais rápido.

Esses insights iniciais são um excelente ponto de partida. A equipe de Data Science pode aprofundar a análise dessas variáveis para construir modelos preditivos mais precisos e, assim, ajudar a Telecom X a desenvolver estratégias mais eficazes para retenção de clientes, especialmente aqueles com contratos mensais e serviço de fibra óptica.
