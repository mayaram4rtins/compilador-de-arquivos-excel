# Compilador de arquivos em Excel
Compilador de arquivos em excel de um projeto individual de automação

A ideia central do projeto é construir um código que une arquivos do excel em um único arquivo final grande demais para ser aberto no computador. Esse arquivo final é necessário para ser importado em um sistema que irá o ler. 

O código tem algumas ideias centrais necessárias para a ideia central para a pessoa que usuaria o código:

1. Soma de formulário = Vendas PDV 

Abrir a base e somar valor contábil e ICMS crédito/débito que são de "Formulário: Venda PDV" na mesma data de "Movimento" e da mesma "Empresa".

Em seguida, abrir a coluna de PIS DÉBITO e COFINS DÉBITO e somar tudo que tiver "Formulário: {vazio}" na mesma data de "Movimento" e da mesma "Empresa".

Paga arquivos diferentes de Vendas PDV, trazer valores individualizados

2. Arquivo final

(ICMS E VALOR CONTABIL) Pegar a colunas: formulário, NF numero, nome, ICMS crédito/débito e Valor Contábil (excluir linhas de valor e icms = 0)
(PIS E CONFINS) Pegar a colunas: formulário, NF numero, nome, PIS e COFINS. (excluir linhas de pis credito e debito e confins credito e debito = 0) - Se tiver qualquer um dos 4 valores preenchidos, manter.

#### dePara_VlrContábil_e_ICMS = {'Vendas PDV':''
    
}

Vendas PDV: contábil credito: 319, contabil debito 37
ICMS s/ Vendas PDV: contabil credito: 243, contabil debito 327
PIS s/ Vendas PDV: credito 246, debito 329
COFINS s/ Vendas PDV: credito 241, debito 326
Nota de Devolução de Compras + NF e coluna numero + coluna nome: credito 80, debito 204
    
Digitação de NF de Faturamento + NF e coluna numero + coluna nome (saída):  
    Se CFOPS 5927, debito 592, credito 80
    Se CFOPS diferente de 5927 mas o NOME é DrogaEx, credito 80, debito 92
    Se CFOPS diferente de tudo isso, credito 341, debito 144
    
ICMS s/ Digitação de NF de Faturamento + NF e coluna numero + coluna nome (saída): credito 243, debito 347

Digitação de NF de Faturamento + NF e coluna numero + coluna nome (entrada):  
    Se o NOME é DrogaEx, credito 93, debito 80
    Se o NOME diferente de DrogaEX, credito 10000, debito 20000
    
ICMS s/ Digitação de NF de Faturamento + NF e coluna numero + coluna nome (entradas): credito 80, debito 59

Devolução de Produtos Caixas + NF e coluna numero + coluna nome: credito 41, debito 332
ICMS s/ Devolução de Produtos Caixas + NF e coluna numero + coluna nome: credito 80, debito 59

Nota Fiscal de Compra e Outras Entradas + NF e coluna numero + coluna nome: 
    Se o NOME é DBR ou conter, credito 10055 e debito 374
    Se o NOME é ou contém BETOFARMA, DELMAR, DOTTO, DEMAC, DROGAEX, EX NG, POA, METROFARMA,    MIYAFARMA, NOVA CAIEIRAS e DROGAROMERO, credito 217 e debito 80
    Se o NOME é diferente disso tudo, credito 204, debito 80
    
ICMS s/ Nota Fiscal de Compra e Outras Entradas + NF e coluna numero + coluna nome: credito 80, debito 59

#### dePara_VlrContábil_e_ICMS = {'Vendas PDV':''
    
}

Tudo que for TIPO E/S: E, PIS (debito 63 e credito 80) e COFINS (debito 57 e credito 80)

Tudo que for TIPO E/S: S, PIS (debito 63 e credito 80) e COFINS (debito 57 e credito 80)
    PIS: Digitação de NF de Faturamento + NF e coluna numero + coluna nome (saída): credito 246, debito 349
    COFINS: Digitação de NF de Faturamento + NF e coluna numero + coluna nome (saída): credito 241, debito 346
    
COLUNAS FINAIS
DATA, Cód. Contabil Débito, Cód. Contabil Crédito, Valor, Cód. Histórico = 1, Complemento Histórico NOME/FORMULÁRIO DO DEPARA, Inicia Lote = 1, Código Matriz/Filial (nº da empresa + 22000), Centro de Custo Débito e Centro de Custo Crédito

4. Nome final do arquivo

Fiscal_NomeDaEmpresa em csv.
