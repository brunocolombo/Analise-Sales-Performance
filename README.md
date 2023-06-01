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
- Orders(Tabela Fato)
- Clientes
- Localização
- Produtos
- Categorias
- Fretes

A Tabela Fato, contém dados de cada ordem, como ID da Ordem, ID Produto, ID Cliente, ID Frete, Data da compra, Data de Entrega, Valor da Compra, Tempo Entrega.

As 4 Tabelas Dimensões contém: Clientes(ID Cliente; Segmento), Localização( ID Ordem; Cidade; Estado), Produtos(ID Produto; Categoria; Sub-Categoria), Frete(ID Frete; Tipo de Frete).

<img src="https://github.com/brunocolombo/Analise-Sales-Performance/assets/77849519/ea4a2897-a542-475c-9b57-1a9e7d6303e5" width="60%">

## Além das tabelas obtidas do Dataset, foi feita uma Tabela Calendário com DAX no Power BI.
![Captura de tela 2023-06-01 140045](https://github.com/brunocolombo/Analise-Sales-Performance/assets/77849519/e3c563b5-e8bd-4260-99aa-9c83925bd46f)

## Perguntas feitas
Para chegar ao resultado final foram elaboradas perguntas para guiar a Análise:

**1 - Como é a tendência das vendas ao longo do tempo?**

**2 - Quias as Categorias e Sub-Categorias que mais venderam ?**

**3 - Quais Estados mais contribuiram para as vendas?**

**4 - Como está a entrega das mercadorias? A maioria está dentro do prazo médio?**

**5 - Quais estados tem o maior tempo de Entrega?**

**6 - Existe sasonalidade nas vendas?**


## Carregando e Explorando os dados no MySQL

## Carregando os dados para o MySQL
- Upload de todas as tabelas(em formato csv.) para podermos analisar e correlacionar os dados.
```sql
load data local infile "C:\\Users\\bruno\\Documents\\Sales_datasets\\Orders.csv"
into table orders_dataset
FIELDS TERMINATED BY ',' ENCLOSED BY '"'
ignore 1 rows;
```

### Analisando os dados
- Numero de Orders
```sql
SELECT
COUNT(distinct OrderID)
FROM orders;

4922
```


- Valor Médio de Compra
```sql
SELECT
ROUND(AVG(Sales),2)
FROM orders;

230.77
```

- Compra de Maior Valor
```sql
SELECT
MAX(Sales)
FROM orders;

22,638.48
```

- Compra de Menos Valor
```sql
SELECT
MIN(Sales)
FROM orders;

0.45
```

- Desvio Padrão dos valores de compra
```sql
SELECT 
ROUND(stddev(Sales),2)
FROM orders;

626.62
```

- Total de Clientes
```sql
SELECT
COUNT(distinct CustomerID)
FROM customers;

793
```

- Total de Clientes
```sql
SELECT
COUNT(DISTINCT ProductID)
FROM products;

1861
```

- Valor Médio de Vendas por Categoria
```sql
SELECT
p.Category,
AVG(Sales)
FROM orders o
JOIN products p ON o.ProductID = p.ProductID
GROUP BY p.Category;

Furniture	 350.65
Office Supplies	119.38
Technology	456.40
```

## Insights retirados da análise:

**1 - Apesar de ser só 18% das vendas totais,Tecnologia é responsavél por 36%($827mil) da Receita Total, tendo também um Valor Médio de Venda de $456, maior que a Média geral de $230.**

**2 - O Q4 foi o melhor período de vendas em todos os anos, que pode ser atribuido a ele ter datas fortes para o comércio como Natal e Black Friday.**

**3 - Os estados que mais trouxeram receitas foram a California e Nova York.**
  
**4 -  O estado da Flórida se mostrou muito forte nas vendas do segmento de Home Office, principalmente no ano de 2015(Top 1).**
  
## Dashboard Power BI
### Com o Power BI, e linguagem DAX utilizaremos gráficos interativos para melhor analisar  e visualizar os dados, e retirar os Insights necessários para responder as perguntas.

<img src="https://github.com/brunocolombo/Analise-Sales-Performance/assets/77849519/59f976da-4d93-4487-8180-70e291bec25c" width="40%">
<img src="https://github.com/brunocolombo/Analise-Sales-Performance/assets/77849519/e96643cd-c2ad-4972-a2bf-ebe536ed0d1b" width="40%">
<img src="https://github.com/brunocolombo/Analise-Sales-Performance/assets/77849519/6f003718-bf5b-4361-92db-3106b6f7f299" width="40%">
<img src="https://github.com/brunocolombo/Analise-Sales-Performance/assets/77849519/0b3c3198-e69e-48c0-98b5-8a29dc05c2df" width="40%">

Você pode acessar o Dashboard clicando aqui <a href="https://app.powerbi.com/view?r=eyJrIjoiYzg5NGE4YjItMmY5MC00ZDQ1LTk3YTQtYmYxYTEyN2ZhYjMwIiwidCI6ImYxMWY0YzkwLTYzZjQtNGE3Ni1hMTVkLTU5YzZlZDQ0ZmM0MSJ9&pageName=ReportSection">Análise Sales Performance<a>.

## Algumas Medidas e coluna criadas com DAX para analisar os dados:
### Receita Acumulada no perído. 
<img src="https://github.com/brunocolombo/Analise-Sales-Performance/assets/77849519/4cbdf1a9-e3e7-454d-abaf-4fd3c920c6f0" width="30%">

### Diferença(%) da Receita em comparação a Receita do período anterior.
<img src="https://github.com/brunocolombo/Analise-Sales-Performance/assets/77849519/68f72405-35bd-451f-af22-6c47786732ac" width="30%">

### Receita do Período anterior ao comparado.
<img src="https://github.com/brunocolombo/Analise-Sales-Performance/assets/77849519/3cbafedb-0dd7-4112-8dc2-4f8fc058f5f1" width="30%">

### Coluna com o tempo de entrega de cada pedido.
<img src="https://github.com/brunocolombo/Analise-Sales-Performance/assets/77849519/7ec0ff84-fc90-4d77-9847-fcfde483e5d1" width="60%">

### Filtro dos Top 5 Estados com maior tempo de entrega em relação a média
<img src="https://github.com/brunocolombo/Analise-Sales-Performance/assets/77849519/a9d512c6-2c39-4188-8bff-3153d4ac0362" width="60%">
