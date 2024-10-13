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
