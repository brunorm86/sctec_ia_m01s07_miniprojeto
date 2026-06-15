# Projeto de ETL Olist - Tratamento de Dados

## Descrição do Projeto

Este projeto consiste no desenvolvimento de um notebook Jupyter para a construção de um pipeline de ETL (Extração, Transformação e Carga) voltado para os dados da empresa Olist. O objetivo principal é sanitizar e estruturar os conjuntos de dados `olist_products_dataset.csv` e `olist_orders_dataset.csv`.

Utilizando exclusivamente bibliotecas nativas do Python (`csv`, `re`, `os` e `datetime`), o sistema soluciona inconsistências e aplica regras de negócio. 

### Principais Transformações e Validações:

- **Sanitização de Categorias (`olist_products_dataset.csv`)**: Conversão para letras minúsculas, remoção de espaços excedentes e caracteres especiais utilizando Expressões Regulares (RegEx). Valores nulos ou vazios são preenchidos com "Sem Categoria".
- **Tratamento de Dimensões Físicas**: Preenchimento de atributos de dimensões ou pesos nulos/vazios com o valor padrão numérico em string `0.0`.
- **Padronização de Datas (`olist_orders_dataset.csv`)**: Conversão das datas de aprovação de pedidos do formato timestamp para o formato `DD/MM/YYYY`.
- **Validação de Hipótese de Negócio**: O algoritmo verifica a hipótese da diretoria de que "datas de entrega estão nulas obrigatoriamente porque o pedido foi cancelado". O script analisa as ocorrências e emite um veredito no relatório de status final, contabilizando entregas vazias para pedidos cancelados e não cancelados.

## Guia de Execução

1. Certifique-se de ter o Python 3.x e o Jupyter instalados em sua máquina.
2. Certifique-se de que os dados estejam localizados na pasta `data_repo/` no mesmo diretório do notebook:
   - `data_repo/olist_products_dataset.csv`
   - `data_repo/olist_orders_dataset.csv`
3. Abra o notebook `main.ipynb` utilizando o Jupyter Notebook, JupyterLab ou VS Code.
4. Execute as células na ordem em que aparecem.
5. O notebook irá processar os dados e gerar dois novos arquivos devidamente sanitizados: `data_repo/olist_products_dataset_tratado.csv` e `data_repo/olist_orders_dataset_tratado.csv`.
6. O relatório de status e estatísticas será impresso no final do notebook.

## Reflexão Teórica: Machine Learning e Qualidade dos Dados

Uma lógica de programação aplicada à limpeza correta dos dados (ETL) é a principal defesa contra o princípio fundamental do *Garbage In, Garbage Out*. Ao lidar com atributos inconsistentes — como categorias com caracteres especiais soltos, registros parcialmente nulos ou formatos de datas incorretos — evitamos que os algoritmos de Machine Learning interpretem esses erros como padrões relevantes. Quando modelos estatísticos ou de Deep Learning treinam sobre um *dataset* despadronizado, as correlações aprendidas tornam-se ruidosas. Por exemplo, uma mesma categoria escrita como "Móveis!" e "moveis" será lida pelo modelo como duas *features* distintas, fragmentando o poder preditivo e dispersando pesos que deveriam ser unificados.

Além disso, o tratamento consciente dos registros nulos, como foi feito com a imputação de `0.0` nas dimensões físicas, ajuda a prevenir vieses severos. Se descartássemos as linhas de produtos sem dimensões físicas sem critério, poderíamos inadvertidamente remover classes inteiras de produtos digitais ou imateriais, causando **Overfitting** nas classes restantes. O modelo final tornar-se-ia "viciado" em predizer e focar apenas em produtos físicos superespecificados, e perderia a generalização necessária para atuar de forma justa e abrangente quando novos padrões invisíveis fossem apresentados na produção.

## Disclaimer: Uso de Inteligência Artificial

A estruturação, documentação e refatoração deste projeto foram realizadas com o suporte de ferramentas de Inteligência Artificial Generativa atuando como um assistente de *pair programming*. A IA foi instruída e supervisionada para atuar dentro de rígidos parâmetros estabelecidos pelo desafio, auxiliando na escrita do código-fonte nativo, formatação da documentação em Markdown e testes lógicos. Todo o algoritmo final passou por validação humana para certificar que a manipulação de dados, estruturas de repetição e conversões matemáticas convergem corretamente e atestam o domínio das lógicas nativas da linguagem Python.
