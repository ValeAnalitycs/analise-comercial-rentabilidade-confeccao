# Medidas DAX

Projeto: **Análise Comercial e Rentabilidade — Confecção**

Este documento reúne as principais medidas DAX utilizadas no dashboard.

As medidas financeiras consideram apenas as linhas válidas para análise,
mantendo os registros problemáticos na base para fins de auditoria e qualidade dos dados.

Filtro aplicado nas medidas financeiras:

```DAX
Fato_Vendas_Confeccao[Linha Para Análise] = "Sim"
```

---

## Medidas Financeiras

### Faturamento Total

```DAX
Faturamento Total =
CALCULATE(
    SUM(Fato_Vendas_Confeccao[Faturamento]),
    Fato_Vendas_Confeccao[Linha Para Análise] = "Sim"
)
```

### Custo Total

```DAX
Custo Total =
CALCULATE(
    SUM(Fato_Vendas_Confeccao[Custo Total]),
    Fato_Vendas_Confeccao[Linha Para Análise] = "Sim"
)
```

### Lucro Total

```DAX
Lucro Total =
CALCULATE(
    SUM(Fato_Vendas_Confeccao[Lucro]),
    Fato_Vendas_Confeccao[Linha Para Análise] = "Sim"
)
```

### Margem %

```DAX
Margem % =
DIVIDE(
    [Lucro Total],
    [Faturamento Total]
)
```

### Quantidade Vendida

```DAX
Quantidade Vendida =
CALCULATE(
    SUM(Fato_Vendas_Confeccao[Quantidade Limpa]),
    Fato_Vendas_Confeccao[Linha Para Análise] = "Sim"
)
```

### Total de Pedidos

```DAX
Total de Pedidos =
CALCULATE(
    DISTINCTCOUNT(Fato_Vendas_Confeccao[ID Pedido]),
    Fato_Vendas_Confeccao[Linha Para Análise] = "Sim"
)
```

### Ticket Médio

```DAX
Ticket Médio =
DIVIDE(
    [Faturamento Total],
    [Total de Pedidos]
)
```

### Custo Médio por Pedido

```DAX
Custo Médio por Pedido =
DIVIDE(
    [Custo Total],
    [Total de Pedidos]
)
```

### Lucro Médio por Pedido

```DAX
Lucro Médio por Pedido =
DIVIDE(
    [Lucro Total],
    [Total de Pedidos]
)
```

### Preço Médio Unitário

```DAX
Preço Médio Unitário =
DIVIDE(
    [Faturamento Total],
    [Quantidade Vendida]
)
```

### Custo Médio Unitário

```DAX
Custo Médio Unitário =
DIVIDE(
    [Custo Total],
    [Quantidade Vendida]
)
```

### Lucro Médio Unitário

```DAX
Lucro Médio Unitário =
DIVIDE(
    [Lucro Total],
    [Quantidade Vendida]
)
```

### Produtos Vendidos

```DAX
Produtos Vendidos =
CALCULATE(
    DISTINCTCOUNT(Fato_Vendas_Confeccao[Produto]),
    Fato_Vendas_Confeccao[Linha Para Análise] = "Sim"
)
```

### Categorias Vendidas

```DAX
Categorias Vendidas =
CALCULATE(
    DISTINCTCOUNT(Fato_Vendas_Confeccao[Categoria]),
    Fato_Vendas_Confeccao[Linha Para Análise] = "Sim"
)
```

### Pedidos com Prejuízo

```DAX
Pedidos com Prejuízo =
CALCULATE(
    DISTINCTCOUNT(Fato_Vendas_Confeccao[ID Pedido]),
    Fato_Vendas_Confeccao[Linha Para Análise] = "Sim",
    Fato_Vendas_Confeccao[Lucro] < 0
)
```

### % Pedidos com Prejuízo

```DAX
% Pedidos com Prejuízo =
DIVIDE(
    [Pedidos com Prejuízo],
    [Total de Pedidos]
)
```

---

## Medidas de Qualidade dos Dados

### Total de Linhas

```DAX
Total de Linhas =
COUNTROWS(Fato_Vendas_Confeccao)
```

### Linhas Válidas

```DAX
Linhas Válidas =
CALCULATE(
    COUNTROWS(Fato_Vendas_Confeccao),
    Fato_Vendas_Confeccao[Status Geral] = "Linha válida"
)
```

### Linhas Inválidas

```DAX
Linhas Inválidas =
CALCULATE(
    COUNTROWS(Fato_Vendas_Confeccao),
    Fato_Vendas_Confeccao[Status Geral] = "Linha inválida"
)
```

### % Linhas Válidas

```DAX
% Linhas Válidas =
DIVIDE(
    [Linhas Válidas],
    [Total de Linhas]
)
```

### % Linhas Inválidas

```DAX
% Linhas Inválidas =
DIVIDE(
    [Linhas Inválidas],
    [Total de Linhas]
)
```

---

## Observação

A modelagem preserva as linhas inconsistentes da base original, mas impede que elas contaminem os indicadores financeiros.

Essa abordagem permite analisar os resultados comerciais e, ao mesmo tempo, demonstrar a qualidade dos dados utilizados na construção do dashboard.
