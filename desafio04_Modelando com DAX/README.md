## Projeto: Processamento de Dados com Power BI

### Objetivo:
Criar um modelo de dados baseado em star schema usando a tabela *Financial Sample*. A estrutura foi dividida em tabelas dimensão e uma tabela fato, com o intuito de melhorar a performance analítica.

### Etapas:
1. Criação de tabelas dimensões (*D_Produtos*, *D_Produtos_Detalhes*, etc.).
2. Uso de funções DAX para calcular médias, medianas e outros indicadores.
3. Criação da tabela fato (*F_Vendas*) e das relações entre as tabelas.
4. Criação de uma tabela de calendário utilizando DAX (`calendar()`).
5. Reorganização e validação do modelo final.

### Funcionalidades DAX Utilizadas:
- `AVERAGE()`
- `MEDIAN()`
- `MAX()`
- `MIN()`
- `CALENDAR()`

- D_Produtos = 
SUMMARIZE(
    'financials',
    'financials'[Product],
    "Média de Unidades Vendidas", AVERAGE('financials'[Units Sold]),
    "Média do Valor de Vendas", AVERAGE('financials'[Sales]),
    "Mediana do Valor de Vendas", MEDIAN('financials'[Sales]),
    "Valor Máximo de Venda", MAX('financials'[Sales]),
    "Valor Mínimo de Venda", MIN('financials'[Sales])
)

D_Produtos_Detalhes =  
SUMMARIZE(
    'financials',
    'financials'[Product],
    "Discount Band", MAX('financials'[Discount Band]),
    "Sale Price", MAX('financials'[Sales Price]),
    "Units Sold", SUM('financials'[Units Sold]),
    "Manufacturing Price", MAX('financials'[Manufacturing Price])
)

D_Descontos = 
SUMMARIZE(
    'financials',
    'financials'[Product],
    "Discount", MAX('financials'[Discount]),
    "Discount Band", MAX('financials'[Discount Band])
)

F_Vendas = 
SELECTCOLUMNS(
    'financials',
    "ID_Produto", 'financials'[Product],
    "Produto", 'financials'[Product],
    "Units Sold", 'financials'[Units Sold],
    "Sales Price", 'financials'[Sales Price],
    "Discount", 'financials'[Discount],
    "Band", 'financials'[Discount Band],
    "Segment", 'financials'[Segment],
    "Country", 'financials'[Country],
    "Sales", 'financials'[Sales],
    "Profit", 'financials'[Profit],
    "Date", 'financials'[Date]
)

D_Calendário = CALENDAR(MIN('financials'[Date]), MAX('financials'[Date]))

