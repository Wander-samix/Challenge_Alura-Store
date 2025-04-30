# Vendas por Categoria e Loja

Este repositório contém scripts em Python para:  
- Carregar e concatenar dados de vendas de quatro lojas diferentes  
- Analisar métricas como contagem de vendas, faturamento total, frete médio e avaliação média por loja  
- Gerar gráficos de barras e mapas de dispersão para visualização dessas métricas  

## 1. Pré-requisitos

- Python 3.7 ou superior  
- Bibliotecas Python:
  - pandas
  - matplotlib

Você pode instalar as dependências executando:

bash
pip install pandas matplotlib


## 2. Estrutura de Dados

Os dados são obtidos diretamente dos arquivos CSV hospedados no GitHub (loja_1.csv, loja_2.csv, loja_3.csv, loja_4.csv). Cada arquivo possui colunas como:

- `Data`: data da compra  
- `Preço`: valor da venda (R$)  
- `Frete`: valor do frete (R$)  
- `Avaliação da compra`: nota de 1 a 5 dada pelo cliente  
- `lon`, `lat`: coordenadas geográficas do ponto de venda

## 3. Pipeline de Processamento

1. **Carregamento**: ler cada CSV em um DataFrame com `pd.read_csv(url)` e adicionar a coluna `Loja` para identificar a origem.  
2. **Concatenação**: mesclar os quatro DataFrames em um único `df_all` via `pd.concat`.  
3. **Cálculos**:
   - `vendas_cat`: contagem de vendas por loja e categoria (`df_all.groupby(['Loja', 'Categoria do Produto']).size()`).  
   - `faturamento`: soma dos valores de `Preço` por loja.  
   - `frete_medio`: média de `Frete` por loja.  
   - `media_avaliacao`: média de `Avaliação da compra` por loja.  

## 4. Visualizações

### 4.1 Gráfico de Barras Empilhadas (Contagem por Categoria)

- Pivot em `vendas_cat` para formato de matriz (lojas × categorias).  
- Plot com `kind='bar', stacked=True`.  
- Anotações internas mostrando contagem de cada categoria e total acima de cada barra.  
- Personalização de cores e ajustes de legenda.

### 4.2 Faturamento Total por Loja

- Gráfico de barras verticais ordenado por faturamento decrescente.  
- Formatação de eixo Y em Real brasileiro (`R$`).  
- Anotações de valor no topo de cada barra.

### 4.3 Frete Médio por Loja

- Mesma estrutura do gráfico de faturamento, porém exibindo média de frete.  
- Eixo Y formatado para duas casas decimais.

### 4.4 Avaliação Média por Loja

- Gráfico de barras com barra por loja, escala de 1 a 5.  
- Cores distintas e anotações com duas casas decimais.

### 4.5 Dispersão Geográfica (Scatter Plot)

- Pontos plotados conforme `lon` e `lat`.  
- Tamanho proporcional ao valor de `Preço`.  
- Cores diferentes por loja e legenda fora do gráfico.

## 5. Customização de Paletas de Cores

- As paletas padrão (`tab10`, `tab20`) são utilizadas.  
- É possível pular índices indesejados para evitar sobreposição com cores de barras de loja.  
- Exemplos de geração dinâmica de tons e gradientes por loja estão nos scripts.

## 6. Como Executar

1. Clone este repositório:
   bash
git clone <URL_DO_REPO>
cd nome_do_repositorio

2. Instale dependências:
   bash
pip install pandas matplotlib
  
3. Execute o script principal (exemplo: `plot_vendas.py`):
   bash
python plot_vendas.py  

4. Modifique parâmetros (URLs, divisores de tamanho de bolha, paletas) diretamente no código conforme necessidade.



