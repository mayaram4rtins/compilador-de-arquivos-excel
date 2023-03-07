

 <h1 align="center"> 🗃️ Compilador de arquivos Excel </h1>

<p align="center">
<img src="http://img.shields.io/static/v1?label=STATUS&message=EM%20DESENVOLVIMENTO&color=GREEN&style=for-the-badge"/>
</p>

![Compilador-de-arquivos-excel](https://user-images.githubusercontent.com/91706209/213877765-4869a8c0-a992-4dca-8648-46b432a871f5.png)

# :pushpin: Índice

* [Índice](https://github.com/mayaram4rtins/compilador-de-arquivos-excel#pushpin-índice)
* [Descrição do Projeto](https://github.com/mayaram4rtins/compilador-de-arquivos-excel#page_facing_up-descrição-do-projeto)
* [Funcionalidades do Projeto](https://github.com/mayaram4rtins/compilador-de-arquivos-excel#desktop_computer-funcionalidades-do-projeto)
* [Ferramentas e Linguagens Utilizadas](https://github.com/mayaram4rtins/compilador-de-arquivos-excel#snake-ferramentas-e-linguagem-utilizadas)
* [Pessoas Contribuidoras](#pessoas-contribuidoras)
* [Construção do Projeto](https://github.com/mayaram4rtins/compilador-de-arquivos-excel#hammer-construção-do-projeto)

# :page_facing_up: Descrição do projeto

A ideia central do projeto transformar em arquivos legíveis por um sistema específico através de arquivos em excel que exigem tratamento prévio.
Esse tratamento acaba por levar muito tempo por conta do tamanho dos arquivos e da manualidade do processo. 
Logo, tem-se como objetivo diminuir o tempo de processamento desses dados.

# :desktop_computer: Funcionalidades do projeto

- `Funcionalidade 1`: Diminuição do tempo de processamento dos dados
- `Funcionalidade 2`: Tratamento dos dados

# :snake: Ferramentas e linguagem utilizadas

+ Python 3.11.1.
+ Jupyter Notebook 6.4.12.

# :hammer: Construção do projeto

Antes de construir o arquivo final, deve-se tratar os dados de acordo com as seguintes condições:

1. Somar todas os 'Formulários' cujo valor é Vendas PDV de acordo com: 'Empresa', 'Movimento' das abas do arquivo 'Fiscal_(NomeDaEmpresa)' 

    + Abrir a base e somar valor contábil e ICMS crédito/débito que são de "Formulário: Venda PDV" na mesma data de "Movimento" e da mesma "Empresa".

    + Em seguida, abrir a coluna de PIS DÉBITO e COFINS DÉBITO e somar tudo que tiver "Formulário: {vazio}" na mesma data de "Movimento" e da mesma "Empresa".

Para arquivos diferentes de Vendas PDV, os valores são utilizados sem nenhum tratamento prévio pois são únicos. 

2. Arquivo final

Para o arquivo final, deve-se juntar os arquivos com os dados tratados e os dados únicos. Além disso, deve-se excluir as linhas tais quais os valores de todos os atributos tratados, ou seja ICMS Crédito/Débito, PIS Débito, Cofins Débito, Cofins Crédito, PIS Crédito e Valor Contábil sejam 0 todos ao mesmo tempo.

Por fim, constrói-se o modelo do arquivo, que deve ser .csv, com as seguintes colunas: 

 1. Colunas pré-existentes que foram alteradas:
 
     + DATA = Movimento; 
     + Complemento Histórico = NOME/FORMULÁRIO DO DEPARA;
     + Código Matriz/Filial = nº da empresa + 22000;
     + Valor;
     
 2. Colunas adicionadas e suas parametrizações:
 
     + Cód. Contabil Débito = Condições contidas no DePara();
     + Cód. Contabil Crédito = Condições contidas no DePara();
     + Inicia Lote = 1;
     + Cód. Histórico = 1;
     + Centro de Custo Débito;
     + Centro de Custo Crédito.

3. Dicionário com condições que preencheram as colunas: Cód. Contábil Débito e Crédito.
       
     * Vendas PDV: contábil credito: 319, contabil debito 37;
     * ICMS s/ Vendas PDV: contabil credito: 243, contabil debito 327;
     * PIS s/ Vendas PDV: credito 246, debito 329;
     * COFINS s/ Vendas PDV: credito 241, debito 326;
     * Nota de Devolução de Compras + NF e coluna numero + coluna nome: credito 80, debito 204;
     * Digitação de NF de Faturamento + NF e coluna numero + coluna nome (saída):  
          
          1. Se CFOPS 5927, debito 592, credito 80;
          2. Se CFOPS diferente de 5927 mas o NOME é DrogaEx, credito 80, debito 92;
          3. Se CFOPS diferente de tudo isso, credito 341, debito 144;
    
     * ICMS s/ Digitação de NF de Faturamento + NF e coluna numero + coluna nome (saída): credito 243, debito 347
     * Digitação de NF de Faturamento + NF e coluna numero + coluna nome (entrada):  
     
          1. Se o NOME é DrogaEx, credito 93, debito 80
          2. Se o NOME diferente de DrogaEX, credito 10000, debito 20000
    
     * ICMS s/ Digitação de NF de Faturamento + NF e coluna numero + coluna nome (entradas): credito 80, debito 59

     * Devolução de Produtos Caixas + NF e coluna numero + coluna nome: credito 41, debito 332
     * ICMS s/ Devolução de Produtos Caixas + NF e coluna numero + coluna nome: credito 80, debito 59

     * Nota Fiscal de Compra e Outras Entradas + NF e coluna numero + coluna nome: 
          1. Se o NOME é DBR ou conter, credito 10055 e debito 374
          2. Se o NOME é ou contém BETOFARMA, DELMAR, DOTTO, DEMAC, DROGAEX, EX NG, POA, METROFARMA, MIYAFARMA, NOVA CAIEIRAS e DROGAROMERO, credito 217 e debito 80
          3. Se o NOME é diferente disso tudo, credito 204, debito 80
    
     * ICMS s/ Nota Fiscal de Compra e Outras Entradas + NF e coluna numero + coluna nome: credito 80, debito 59
     * Tudo que for TIPO E/S: E, PIS (debito 63 e credito 80) e COFINS (debito 57 e credito 80)

     * Tudo que for TIPO E/S: S, PIS (debito 63 e credito 80) e COFINS (debito 57 e credito 80)
          1. PIS: Digitação de NF de Faturamento + NF e coluna numero + coluna nome (saída): credito 246, debito 349
          2. COFINS: Digitação de NF de Faturamento + NF e coluna numero + coluna nome (saída): credito 241, debito 346
    
4. Nome final do arquivo

Fiscal_NomeDaEmpresa em csv.
