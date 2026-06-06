# Projeto em Ciência de Dados 2

## Análise Financeira e Modelagem Preditiva com Python e Power BI

Este repositório contém os materiais desenvolvidos para o Projeto em Ciência de Dados 2 do MBA em Ciência de Dados da FM2S Educação e Consultoria.

O projeto tem como objetivo analisar dados financeiros de vendas do dataset público Superstore, identificar fatores que impactam a rentabilidade e desenvolver um dashboard executivo em Power BI para apoio à tomada de decisão.

---

## Objetivo do Projeto

O objetivo principal deste projeto é aplicar técnicas de Ciência de Dados e Business Intelligence para responder à seguinte questão:

**O crescimento das vendas está sendo acompanhado por crescimento real da lucratividade?**

Além disso, o projeto busca investigar:

* Quais fatores mais impactam o lucro;
* Como os descontos afetam a rentabilidade;
* Quais categorias e regiões apresentam melhor desempenho;
* Se é possível prever o lucro com base nos dados históricos;
* Como transformar análises técnicas em informações executivas por meio de dashboard.

---

## Base de Dados

Foi utilizado o dataset público **Sample Superstore**, composto por:

* **9.994 registros**
* **21 colunas**
* Informações de vendas, lucro, desconto, quantidade, categoria, segmento, região e data do pedido.

Principais variáveis utilizadas:

* `Sales` / Receita
* `Profit` / Lucro
* `Discount` / Desconto
* `Quantity` / Quantidade
* `Category` / Categoria
* `Segment` / Segmento
* `Region` / Região
* `Order Date` / Data do Pedido

---

## Etapas Desenvolvidas

### 1. Tratamento dos Dados em Python

A primeira etapa do projeto foi realizada em Python, contemplando:

* Importação da base;
* Verificação da estrutura do dataset;
* Análise dos tipos de dados;
* Conversão de datas;
* Tradução e padronização dos campos;
* Validação de informações;
* Exportação da base tratada para utilização no Power BI.

---

### 2. Análise Exploratória dos Dados (EDA)

A análise exploratória foi desenvolvida com o objetivo de compreender o comportamento das principais variáveis do dataset.

Foram analisados:

* Distribuição da receita;
* Distribuição do lucro;
* Presença de outliers;
* Relação entre receita, lucro, desconto e quantidade;
* Correlação entre variáveis;
* Padrões temporais;
* Diferenças entre categorias, segmentos e regiões.

Visualizações utilizadas:

* Histogramas;
* Boxplots;
* Gráficos de dispersão;
* Heatmap de correlação;
* Gráficos temporais;
* Gráficos categóricos.

---

### 3. Feature Engineering

Foram criadas novas variáveis para enriquecer as análises e apoiar a modelagem preditiva.

Principais variáveis criadas:

* `Ano`
* `Mês`
* `Margem_%`
* `Status_Lucro`
* `Faixa_Desconto`

Essas variáveis permitiram avaliar melhor a rentabilidade, o impacto dos descontos e o comportamento temporal das vendas.

---

### 4. Modelagem Preditiva

Foram desenvolvidos dois modelos de regressão para previsão do lucro:

#### Regressão Linear

Modelo utilizado como baseline para comparação.

Resultado obtido:

* **R² Teste: -0,723**

#### Random Forest Regressor

Modelo utilizado para capturar relações não lineares e analisar a importância das variáveis.

Resultados obtidos:

* **R² Treino: 0,965**
* **R² Teste: -0,064**

Embora o Random Forest também tenha apresentado limitação de generalização, seu desempenho foi superior ao da Regressão Linear.

Além disso, o modelo permitiu identificar os principais fatores associados ao lucro por meio da análise de importância das variáveis.

---

## Interpretação dos Modelos

O valor negativo de R² no conjunto de teste indica que os modelos não apresentaram boa capacidade preditiva para generalização.

No entanto, o Random Forest foi mantido como modelo de referência por dois motivos principais:

1. Apresentou desempenho superior ao modelo de Regressão Linear;
2. Permitiu analisar a importância das variáveis que mais influenciam o lucro.

Principais variáveis identificadas pelo modelo:

* **Receita:** 76,3%
* **Desconto:** 15,6%
* **Quantidade:** 2,3%

A análise reforça que a receita é o principal fator associado ao lucro, enquanto descontos elevados representam um ponto de atenção para a rentabilidade.

---

## Dashboard em Power BI

Após as análises em Python, os resultados foram consolidados em um dashboard executivo desenvolvido em Power BI.

O dashboard foi estruturado em cinco páginas:

### 1. Home

Página inicial com navegação entre os módulos do dashboard.

### 2. Visão Executiva

Apresenta os principais indicadores financeiros:

* Receita Total;
* Lucro Total;
* Margem;
* Quantidade de Pedidos;
* Ticket Médio.

Também inclui análises de lucro por categoria, região e evolução anual.

### 3. Rentabilidade

Página voltada à análise de margem, lucro positivo, lucro negativo e impacto dos descontos.

Um dos principais insights identificados foi que descontos elevados geraram lucro negativo acumulado, indicando risco para a rentabilidade.

### 4. Drivers e Descontos

Página que integra os resultados do Python ao Power BI.

Foram utilizadas informações da modelagem preditiva para apresentar:

* Melhor modelo;
* R² de teste;
* Importância das variáveis;
* Overfitting;
* Correlação entre variáveis.

### 5. Tendências e Mercado

Página voltada à análise temporal, com evolução da receita, lucro, segmentos e sazonalidade mensal.

---

## Integração Python + Power BI

O projeto foi desenvolvido em duas camadas principais:

### Python

Responsável por:

* Tratamento dos dados;
* Análise exploratória;
* Feature Engineering;
* Modelagem preditiva;
* Avaliação dos modelos;
* Geração de insights técnicos.

### Power BI

Responsável por:

* Ajustes complementares no Power Query;
* Construção de medidas DAX;
* Criação de tabelas auxiliares;
* Desenvolvimento do dashboard executivo;
* Visualização dos resultados.

As tabelas auxiliares criadas no Power BI utilizaram informações obtidas no Python, como a importância das variáveis e a comparação entre treino e teste.

---

## Principais Medidas DAX Utilizadas

Algumas das principais medidas criadas no Power BI foram:

```DAX
Receita Total = SUM(Dados[Receita])
```

```DAX
Lucro Total = SUM(Dados[Lucro])
```

```DAX
Margem % =
DIVIDE(
    [Lucro Total],
    [Receita Total]
)
```

```DAX
Qtd Pedidos =
DISTINCTCOUNT(Dados[ID Pedido])
```

```DAX
Ticket Médio =
DIVIDE(
    [Receita Total],
    [Qtd Pedidos]
)
```

```DAX
Lucro Positivo =
CALCULATE(
    SUM(Dados[Lucro]),
    Dados[Lucro] > 0
)
```

```DAX
Lucro Negativo =
CALCULATE(
    SUM(Dados[Lucro]),
    Dados[Lucro] < 0
)
```

---

## Principais Insights

Entre os principais resultados encontrados, destacam-se:

* A receita apresentou crescimento consistente ao longo do período analisado;
* A categoria Tecnologia apresentou o maior lucro acumulado;
* A Região Oeste apresentou melhor desempenho financeiro;
* Descontos elevados impactaram negativamente a rentabilidade;
* A receita foi a variável mais importante para previsão do lucro;
* O desconto foi identificado como principal driver gerenciável;
* O modelo Random Forest apresentou overfitting, com alto desempenho no treino e baixo desempenho no teste.

---

## Ferramentas Utilizadas

* Python
* Pandas
* Matplotlib
* Seaborn
* Scikit-Learn
* Power Query
* Power BI
* GitHub

---

## Autora

**Luana Andia da Costa**
MBA em Ciência de Dados
FM2S Educação e Consultoria
2026

