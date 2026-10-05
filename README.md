# Modelagem e Transformacao de Dados com DAX - Power BI

Projeto desenvolvido para a Formacao Power BI Analyst da DIO, utilizando a base Microsoft Financial Sample.

## Objetivo

Transformar a tabela unica Financial Sample em um modelo dimensional baseado em Star Schema, separando tabela fato e dimensoes e criando uma dimensao calendario com DAX.

## Estrutura criada

- `Financials_origem`: copia da base original para backup; deve ser ocultada no Power BI.
- `D_Produtos`: dimensao agregada por produto com media de unidades vendidas, media/mediana, maximo e minimo de vendas.
- `D_Produtos_Detalhes`: detalhes de produto e condicoes de venda.
- `D_Descontos`: informacoes de descontos por produto.
- `D_Detalhes`: atributos descritivos de Segment e Country que nao foram contemplados nas demais dimensoes.
- `D_Calendario`: criada diretamente no Power BI via DAX com `CALENDAR()`.
- `F_Vendas`: tabela fato com 700 registros de vendas e chaves para as dimensoes.

## ID de Produto

Para reproduzir o exemplo do desafio foi utilizado o seguinte indice:

| Produto | ID_Produto |
|---|---:|
| Carretera | 0 |
| Montana | 1 |
| Paseo | 2 |
| Velo | 3 |
| VTT | 4 |
| Amarilla | 5 |

## DAX utilizado

```DAX
D_Calendario =
ADDCOLUMNS(
    CALENDAR(MIN(F_Vendas[Date]), MAX(F_Vendas[Date])),
    "Ano", YEAR([Date]),
    "MesNumero", MONTH([Date]),
    "MesNome", FORMAT([Date], "mmmm"),
    "Trimestre", "T" & FORMAT([Date], "Q")
)
```

Depois da criacao, `D_Calendario[Date]` deve ser relacionada a `F_Vendas[Date]` em cardinalidade **1 para muitos**.

## Relacionamentos

- `D_Produtos[ID_Produto]` 1:* `F_Vendas[ID_Produto]`
- `D_Produtos_Detalhes[ProdutoDetalheKey]` 1:* `F_Vendas[ProdutoDetalheKey]`
- `D_Descontos[DescontoKey]` 1:* `F_Vendas[DescontoKey]`
- `D_Detalhes[DetalheKey]` 1:* `F_Vendas[DetalheKey]`
- `D_Calendario[Date]` 1:* `F_Vendas[Date]`

As chaves `ProdutoDetalheKey`, `DescontoKey` e `DetalheKey` foram adicionadas como **Surrogate Key** para manter relacionamentos 1:* e evitar muitos-para-muitos.

## Transformacoes realizadas

1. Copia da tabela original para `Financials_origem`.
2. Criacao do indice de produtos.
3. Agrupamento por produto para gerar `D_Produtos`.
4. Calculo de media de unidades vendidas.
5. Calculo de media, mediana, valor maximo e valor minimo de vendas.
6. Criacao das tabelas auxiliares de detalhes, descontos e contexto comercial.
7. Criacao de `SK_ID` para cada registro da fato.
8. Reorganizacao das colunas da tabela fato.
9. Criacao da dimensao calendario usando DAX.
10. Organizacao do Star Schema e definicao das cardinalidades.

## Entrega

O repositorio deve conter:

- arquivo `.pbix`;
- imagem da Exibicao de Modelo com o Star Schema;
- este README;
- opcionalmente a base Excel usada para facilitar a reproducao.

## Fonte dos dados

Microsoft Financial Sample, disponibilizada como material de estudo da Formacao Power BI Analyst da DIO.
