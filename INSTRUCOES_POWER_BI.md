# Passo a passo no Power BI

1. Abra um novo arquivo no Power BI Desktop.
2. Obter Dados > Excel > selecione `modelo_financial_star_schema.xlsx`.
3. Marque `Financials_origem`, `D_Produtos`, `D_Produtos_Detalhes`, `D_Descontos`, `D_Detalhes` e `F_Vendas`.
4. Clique em Carregar.
5. Em Modelagem > Nova tabela, crie `D_Calendario` com o DAX descrito no README.
6. Na Exibicao de Modelo, crie os relacionamentos 1:* listados no README. Direcao de filtro: unica, da dimensao para a fato.
7. Clique com o botao direito em `Financials_origem` e escolha Ocultar na exibicao de relatorio.
8. Posicione `F_Vendas` no centro e as dimensoes ao redor.
9. Salve como `desafio-modelagem-transformacao-dax.pbix`.
10. Tire um print da Exibicao de Modelo e salve como `modelo-star-schema.png`.
