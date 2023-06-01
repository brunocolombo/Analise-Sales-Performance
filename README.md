# Analise-Sales-Performance
A análise é de vendas de quase 5mil ordens, realizadas entre 2015 e 2018.
O objetivo principal é análisar as principais características das vendas, e segmentar os dados para obter Insights.

## Contexto do Projeto
Análisar dados de vendas de uma loja online. Os dados são de quase 5mil vendas realizadas entre 2015 e 2018.

## Dados
Os dados utilizados nesta análise, estavam condensado em uma único Dataset, e foram primeiramente tratados e limpos no Excel.Para conseguir trabalhar com os dados posteriormente no Power BI, foram construidas a partir do Dataset único, 5 Tabelas.


## Ferramentas Utilizdas
- Excel
- -MySQL/ SQL
- Porwer BI

## Tabelas criadas para o Power BI
- Tabela Fato
- Clientes
- Localização
- Produtos
- Categorias
- Fretes

A Tabela Fato, contém dados de cada ordem, como ID da Ordem, ID Produto, ID Cliente, ID Frete, Data da compra, Data de Entrega, Valor da Compra, Tempo Entrega.

As 4 Tabelas Dimensões contém: Clientes(ID Cliente; Segmento), Localização( ID Ordem; Cidade; Estado), Produtos(ID Produto; Categoria; Sub-Categoria), Frete(ID Frete; Tipo de Frete).

Além das tabelas obtidas do Dataset, foi feita uma Tabela Calendário com DAX no Power BI.

## Perguntas feitas
Para chegar ao resultado final foram elaboradas perguntas para guiar a Análise:

**1 - Como é a tendência das vendas ao longo do tempo?**

**2 - Quias as Categorias e Sub-Categorias que mais venderam ?**

**3 - Quais Estados mais contribuiram para as vendas?**

**4 - Como está a entrega das mercadorias? A maioria está dentro do prazo médio?**

**5 - Quais estados tem o maior tempo de Entrega?**

**6 - Existe sasonalidade nas vendas?**



## Carregando os dados para o MySQL
- Upload de todas as tabelas(em formato csv.) para podermos analisar e correlacionar os dados.
```sql
load data local infile "C:\\Users\\bruno\\Documents\\Sales_datasets\\Orders.csv"
into table orders_dataset
FIELDS TERMINATED BY ',' ENCLOSED BY '"'
ignore 1 rows;

## Dashboard Power BI

