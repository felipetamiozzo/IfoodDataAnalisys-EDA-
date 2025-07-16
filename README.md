# Análise Exploratória de Dados (EDA) de Restaurantes iFood

## Visão Geral do Projeto

Este projeto consiste em uma Análise Exploratória de Dados (EDA) completa de um dataset contendo informações sobre restaurantes na plataforma iFood. O objetivo principal é extrair insights valiosos sobre as características dos estabelecimentos, taxas de entrega, tempos de entrega, valores mínimos de pedido e avaliações, utilizando estatística descritiva e visualizações de dados.

## Objetivo

O principal objetivo deste projeto é:

* Realizar uma análise descritiva aprofundada do dataset de restaurantes iFood.

* Identificar padrões, tendências e anomalias nos dados.

* Extrair insights acionáveis que possam ser úteis para a plataforma iFood, restaurantes ou usuários.

* Demonstrar habilidades em manipulação de dados, estatística descritiva e visualização de dados utilizando Python.

## Dados

O dataset utilizado, `ifood-restaurants-february-2021.csv`, contém as seguintes colunas:

* `availableForScheduling`: Indica se o estabelecimento permite o agendamento de pedidos (Booleano).

* `avatar`: URL ou identificador da imagem do perfil/avatar do estabelecimento (Objeto/String).

* `category`: A categoria culinária do estabelecimento (ex: "Japonesa", "Pizza") (Objeto/String).

* `delivery_fee`: O valor da taxa de entrega cobrada pelo estabelecimento (Float).

* `delivery_time`: O tempo estimado de entrega em minutos (Inteiro).

* `distance`: A distância (provavelmente em quilômetros ou metros) entre o ponto de entrega e o estabelecimento (Float).

* `ibge`: O código IBGE da localidade associada ao estabelecimento ou pedido (Inteiro).

* `minimumOrderValue`: O valor mínimo que o pedido deve ter para ser aceito (Float).

* `name`: O nome do estabelecimento (Objeto/String).

* `paymentCodes`: Tipos ou códigos de pagamento aceitos pelo estabelecimento (Objeto/String).

* `price_range`: A faixa de preço do estabelecimento (ex: "CHEAPEST", "CHEAP", "MODERATE", "EXPENSIVE", "MOST_EXPENSIVE") (Objeto/String).

* `rating`: A avaliação média do estabelecimento pelos clientes (Float).

* `tags`: Descritores adicionais ou palavras-chave associadas ao estabelecimento (Objeto/String).

* `url`: A URL direta para a página do estabelecimento no iFood (Objeto/String).

## Metodologia

O projeto segue as seguintes etapas:

1. **Configuração Inicial:** Importação das bibliotecas necessárias (`numpy`, `pandas`, `matplotlib`, `seaborn`) e padronização do estilo das visualizações com `seaborn`.

2. **Carregamento e Inspeção dos Dados:** Leitura do arquivo CSV e uma primeira inspeção das primeiras linhas (`.head()`) e informações gerais do DataFrame (`.info()`, `.shape`).

3. **Seleção de Variáveis:** Foram selecionadas apenas as colunas relevantes para a análise descritiva, removendo aquelas que não contribuíam diretamente para os insights desejados (`avatar`, `ibge`, `name`, `paymentCodes`, `tags`, `url`).

4. **Tratamento de Dados Ausentes e Duplicados:** Verificação de valores nulos e contagem de valores únicos/duplicados. Optou-se por não remover duplicados, considerando o contexto do dataset.

5. **Análise Univariada:**

   * Cálculo de medidas de tendência central (média, mediana) e de dispersão (mínimo, máximo, desvio padrão via `.describe()`) para as variáveis numéricas.

   * Identificação da moda para as variáveis categóricas.

   * Geração de histogramas para as variáveis numéricas e gráficos de contagem para as categóricas, para visualizar a distribuição dos dados.

6. **Tratamento de Outliers:** Identificação e remoção de outliers extremos e valores inconsistentes em `delivery_time`, `minimumOrderValue`, `distance` e `rating` para garantir a precisão das análises subsequentes.

7. **Análise Bivariada:** Exploração das relações entre pares de variáveis, como `price_range` vs `delivery_fee` e `rating`, e `category` vs `delivery_fee`, `delivery_time` e `rating`.

8. **Visualizações:** Criação de diversos gráficos (boxplots, histogramas, countplots, barplots) para ilustrar as distribuições e relações identificadas.

## Análise Exploratória de Dados (EDA) e Insights Principais

### Visão Geral dos Dados

* O dataset original possui mais de 400 mil registros, indicando uma base robusta de informações.

* Após a seleção de variáveis e tratamento de outliers, o DataFrame foi reduzido para cerca de 355 mil registros, focando nas colunas mais relevantes para a análise.

* Não foram encontrados valores nulos nas colunas selecionadas após a limpeza inicial.

### Análise Univariada

#### Taxa de Entrega (`delivery_fee`)

* **Variabilidade Considerável:** A taxa de entrega média é de R$ 6.80, mas com um desvio padrão de R$ 4.31, indicando uma dispersão significativa dos valores.

* **Entrega Grátis:** Existem casos de taxa de entrega zero (R$ 0.00), possivelmente devido a promoções ou ofertas específicas.

* **Outliers:** A maioria das entregas (75%) custa até R$ 9.49, mas há valores extremos de até R$ 35.00, que são raros e foram tratados como outliers.

#### Tempo de Entrega (`delivery_time`)

* **Inconsistências e Outliers:** Foram identificados valores inconsistentes (-1 minuto) e outliers extremos (5050 minutos), que foram removidos para evitar distorções na análise.

* **Experiência Típica:** Para a maioria dos pedidos, 50% das entregas são realizadas em até 45 minutos, e 75% em até 1 hora.

#### Valor Mínimo do Pedido (`minimumOrderValue`)

* **Flexibilidade de Pedido:** Alguns restaurantes permitem pedidos sem valor mínimo (R$ 0.00).

* **Concentração em Valores Baixos:** A maioria dos restaurantes (75%) exige um valor mínimo de pedido de até R$ 20.00.

* **Outlier Extremo:** Um valor de R$ 100.000.000,00 foi identificado como um erro de dados e removido.

#### Avaliação (`rating`)

* A média das avaliações é de 2.52, com uma mediana de 3.96, sugerindo uma distribuição com muitos zeros (restaurantes sem avaliação ou com avaliação padrão zero) e uma concentração de avaliações mais altas entre os que são avaliados. Os zeros foram tratados como outliers.

#### Categorias e Faixa de Preço

* **Agendamento:** A maioria dos estabelecimentos (`availableForScheduling: False`) não permite agendamento de pedidos.

* **Categoria Mais Comum:** "Lanches" é a categoria de restaurante mais frequente no dataset.

* **Faixa de Preço Mais Comum:** A faixa de preço "CHEAPEST" (mais barata) é a mais predominante.

### Análise Bivariada

#### Faixa de Preço (`price_range`) vs. Taxa de Entrega (`delivery_fee`)

* Existe uma correlação positiva: Restaurantes mais caros (`MOST_EXPENSIVE`) tendem a ter taxas de entrega médias mais altas (R$ 9.39), enquanto os mais baratos (`CHEAP`) têm taxas mais baixas (R$ 6.31). Isso sugere que o preço do estabelecimento pode influenciar a estrutura de custos de entrega.

#### Faixa de Preço (`price_range`) vs. Avaliação (`rating`)

* Restaurantes mais caros tendem a ter avaliações médias ligeiramente mais altas. Por exemplo, `MOST_EXPENSIVE` tem uma média de 4.41, enquanto `CHEAPEST` tem 4.19. Embora a diferença seja pequena, indica uma leve percepção de maior qualidade ou satisfação em estabelecimentos de maior valor.

#### Categoria (`category`) vs. Taxa de Entrega (`delivery_fee`)

* Categorias como 'Açougue', 'Padaria' e 'Mercado' apresentam as maiores taxas de entrega médias. Isso pode ser explicado pelo volume, peso ou complexidade da logística de entrega desses tipos de produtos.

#### Categoria (`category`) vs. Tempo de Entrega (`delivery_time`)

* 'Mercado', 'Farmácia' e 'Conveniência' são as categorias com os maiores tempos médios de entrega. Isso pode estar relacionado à maior variedade de itens, processos de separação mais demorados ou distâncias maiores para entrega de compras.

#### Categoria (`category`) vs. Avaliação (`rating`)

* Categorias como 'Japonesa', 'Brasileira' e 'Italiana' estão entre as mais bem avaliadas. Isso pode indicar uma alta satisfação do cliente com a qualidade da comida ou do serviço nessas culinárias específicas.

## Tratamento de Outliers

O tratamento de outliers foi crucial para garantir a robustez das análises. Foram removidos:

* Tempos de entrega negativos e acima de 120 minutos.

* Valores mínimos de pedido acima de R$ 500.

* Distâncias acima de 100 km.

* Avaliações iguais a 0.0 (consideradas como ausência de avaliação significativa).

Este processo resultou em um dataset mais limpo e representativo para a análise descritiva.

## Conclusões

A Análise Exploratória de Dados revelou insights importantes sobre o comportamento dos restaurantes no iFood:

* Há uma clara relação entre a faixa de preço do restaurante e suas taxas de entrega e avaliações.

* As categorias de restaurantes impactam significativamente as taxas e tempos de entrega, bem como a satisfação do cliente.

* A qualidade dos dados é um fator crítico, e a identificação e tratamento de outliers são etapas fundamentais em qualquer projeto de análise de dados.

Este projeto serve como uma base sólida para futuras análises, como modelagem preditiva de tempo de entrega, otimização de taxas ou segmentação de mercado.

## Tecnologias Utilizadas

* **Python**

* **Pandas:** Para manipulação e análise de dados.

* **NumPy:** Para operações numéricas.

* **Matplotlib:** Para visualização de dados.

* **Seaborn:** Para visualizações estatísticas e padronização de gráficos.

* **Jupyter Notebook:** Para o desenvolvimento interativo e apresentação da análise.


# Análise Exploratória de Dados (EDA) de Restaurantes iFood

## Visão Geral do Projeto

Este projeto consiste em uma Análise Exploratória de Dados (EDA) completa de um dataset contendo informações sobre restaurantes na plataforma iFood. O objetivo principal é extrair insights valiosos sobre as características dos estabelecimentos, taxas de entrega, tempos de entrega, valores mínimos de pedido e avaliações, utilizando estatística descritiva e visualizações de dados.

## Objetivo

O principal objetivo deste projeto é:

* Realizar uma análise descritiva aprofundada do dataset de restaurantes iFood.

* Identificar padrões, tendências e anomalias nos dados.

* Extrair insights acionáveis que possam ser úteis para a plataforma iFood, restaurantes ou usuários.

* Demonstrar habilidades em manipulação de dados, estatística descritiva e visualização de dados utilizando Python.

## Dados

O dataset utilizado, `ifood-restaurants-february-2021.csv`, contém as seguintes colunas:

* `availableForScheduling`: Indica se o estabelecimento permite o agendamento de pedidos (Booleano).

* `avatar`: URL ou identificador da imagem do perfil/avatar do estabelecimento (Objeto/String).

* `category`: A categoria culinária do estabelecimento (ex: "Japonesa", "Pizza") (Objeto/String).

* `delivery_fee`: O valor da taxa de entrega cobrada pelo estabelecimento (Float).

* `delivery_time`: O tempo estimado de entrega em minutos (Inteiro).

* `distance`: A distância (provavelmente em quilômetros ou metros) entre o ponto de entrega e o estabelecimento (Float).

* `ibge`: O código IBGE da localidade associada ao estabelecimento ou pedido (Inteiro).

* `minimumOrderValue`: O valor mínimo que o pedido deve ter para ser aceito (Float).

* `name`: O nome do estabelecimento (Objeto/String).

* `paymentCodes`: Tipos ou códigos de pagamento aceitos pelo estabelecimento (Objeto/String).

* `price_range`: A faixa de preço do estabelecimento (ex: "CHEAPEST", "CHEAP", "MODERATE", "EXPENSIVE", "MOST_EXPENSIVE") (Objeto/String).

* `rating`: A avaliação média do estabelecimento pelos clientes (Float).

* `tags`: Descritores adicionais ou palavras-chave associadas ao estabelecimento (Objeto/String).

* `url`: A URL direta para a página do estabelecimento no iFood (Objeto/String).

## Metodologia

O projeto segue as seguintes etapas:

1. **Configuração Inicial:** Importação das bibliotecas necessárias (`numpy`, `pandas`, `matplotlib`, `seaborn`) e padronização do estilo das visualizações com `seaborn`.

2. **Carregamento e Inspeção dos Dados:** Leitura do arquivo CSV e uma primeira inspeção das primeiras linhas (`.head()`) e informações gerais do DataFrame (`.info()`, `.shape`).

3. **Seleção de Variáveis:** Foram selecionadas apenas as colunas relevantes para a análise descritiva, removendo aquelas que não contribuíam diretamente para os insights desejados (`avatar`, `ibge`, `name`, `paymentCodes`, `tags`, `url`).

4. **Tratamento de Dados Ausentes e Duplicados:** Verificação de valores nulos e contagem de valores únicos/duplicados. Optou-se por não remover duplicados, considerando o contexto do dataset.

5. **Análise Univariada:**

   * Cálculo de medidas de tendência central (média, mediana) e de dispersão (mínimo, máximo, desvio padrão via `.describe()`) para as variáveis numéricas.

   * Identificação da moda para as variáveis categóricas.

   * Geração de histogramas para as variáveis numéricas e gráficos de contagem para as categóricas, para visualizar a distribuição dos dados.

6. **Tratamento de Outliers:** Identificação e remoção de outliers extremos e valores inconsistentes em `delivery_time`, `minimumOrderValue`, `distance` e `rating` para garantir a precisão das análises subsequentes.

7. **Análise Bivariada:** Exploração das relações entre pares de variáveis, como `price_range` vs `delivery_fee` e `rating`, e `category` vs `delivery_fee`, `delivery_time` e `rating`.

8. **Visualizações:** Criação de diversos gráficos (boxplots, histogramas, countplots, barplots) para ilustrar as distribuições e relações identificadas.

## Análise Exploratória de Dados (EDA) e Insights Principais

### Visão Geral dos Dados

* O dataset original possui mais de 400 mil registros, indicando uma base robusta de informações.

* Após a seleção de variáveis e tratamento de outliers, o DataFrame foi reduzido para cerca de 355 mil registros, focando nas colunas mais relevantes para a análise.

* Não foram encontrados valores nulos nas colunas selecionadas após a limpeza inicial.

### Análise Univariada

#### Taxa de Entrega (`delivery_fee`)

* **Variabilidade Considerável:** A taxa de entrega média é de R$ 6.80, mas com um desvio padrão de R$ 4.31, indicando uma dispersão significativa dos valores.

* **Entrega Grátis:** Existem casos de taxa de entrega zero (R$ 0.00), possivelmente devido a promoções ou ofertas específicas.

* **Outliers:** A maioria das entregas (75%) custa até R$ 9.49, mas há valores extremos de até R$ 35.00, que são raros e foram tratados como outliers.

#### Tempo de Entrega (`delivery_time`)

* **Inconsistências e Outliers:** Foram identificados valores inconsistentes (-1 minuto) e outliers extremos (5050 minutos), que foram removidos para evitar distorções na análise.

* **Experiência Típica:** Para a maioria dos pedidos, 50% das entregas são realizadas em até 45 minutos, e 75% em até 1 hora.

#### Valor Mínimo do Pedido (`minimumOrderValue`)

* **Flexibilidade de Pedido:** Alguns restaurantes permitem pedidos sem valor mínimo (R$ 0.00).

* **Concentração em Valores Baixos:** A maioria dos restaurantes (75%) exige um valor mínimo de pedido de até R$ 20.00.

* **Outlier Extremo:** Um valor de R$ 100.000.000,00 foi identificado como um erro de dados e removido.

#### Avaliação (`rating`)

* A média das avaliações é de 2.52, com uma mediana de 3.96, sugerindo uma distribuição com muitos zeros (restaurantes sem avaliação ou com avaliação padrão zero) e uma concentração de avaliações mais altas entre os que são avaliados. Os zeros foram tratados como outliers.

#### Categorias e Faixa de Preço

* **Agendamento:** A maioria dos estabelecimentos (`availableForScheduling: False`) não permite agendamento de pedidos.

* **Categoria Mais Comum:** "Lanches" é a categoria de restaurante mais frequente no dataset.

* **Faixa de Preço Mais Comum:** A faixa de preço "CHEAPEST" (mais barata) é a mais predominante.

### Análise Bivariada

#### Faixa de Preço (`price_range`) vs. Taxa de Entrega (`delivery_fee`)

* Existe uma correlação positiva: Restaurantes mais caros (`MOST_EXPENSIVE`) tendem a ter taxas de entrega médias mais altas (R$ 9.39), enquanto os mais baratos (`CHEAP`) têm taxas mais baixas (R$ 6.31). Isso sugere que o preço do estabelecimento pode influenciar a estrutura de custos de entrega.

#### Faixa de Preço (`price_range`) vs. Avaliação (`rating`)

* Restaurantes mais caros tendem a ter avaliações médias ligeiramente mais altas. Por exemplo, `MOST_EXPENSIVE` tem uma média de 4.41, enquanto `CHEAPEST` tem 4.19. Embora a diferença seja pequena, indica uma leve percepção de maior qualidade ou satisfação em estabelecimentos de maior valor.

#### Categoria (`category`) vs. Taxa de Entrega (`delivery_fee`)

* Categorias como 'Açougue', 'Padaria' e 'Mercado' apresentam as maiores taxas de entrega médias. Isso pode ser explicado pelo volume, peso ou complexidade da logística de entrega desses tipos de produtos.

#### Categoria (`category`) vs. Tempo de Entrega (`delivery_time`)

* 'Mercado', 'Farmácia' e 'Conveniência' são as categorias com os maiores tempos médios de entrega. Isso pode estar relacionado à maior variedade de itens, processos de separação mais demorados ou distâncias maiores para entrega de compras.

#### Categoria (`category`) vs. Avaliação (`rating`)

* Categorias como 'Japonesa', 'Brasileira' e 'Italiana' estão entre as mais bem avaliadas. Isso pode indicar uma alta satisfação do cliente com a qualidade da comida ou do serviço nessas culinárias específicas.

## Tratamento de Outliers

O tratamento de outliers foi crucial para garantir a robustez das análises. Foram removidos:

* Tempos de entrega negativos e acima de 120 minutos.

* Valores mínimos de pedido acima de R$ 500.

* Distâncias acima de 100 km.

* Avaliações iguais a 0.0 (consideradas como ausência de avaliação significativa).

Este processo resultou em um dataset mais limpo e representativo para a análise descritiva.

## Conclusões

A Análise Exploratória de Dados revelou insights importantes sobre o comportamento dos restaurantes no iFood:

* Há uma clara relação entre a faixa de preço do restaurante e suas taxas de entrega e avaliações.

* As categorias de restaurantes impactam significativamente as taxas e tempos de entrega, bem como a satisfação do cliente.

* A qualidade dos dados é um fator crítico, e a identificação e tratamento de outliers são etapas fundamentais em qualquer projeto de análise de dados.

Este projeto serve como uma base sólida para futuras análises, como modelagem preditiva de tempo de entrega, otimização de taxas ou segmentação de mercado.

## Tecnologias Utilizadas

* **Python**

* **Pandas:** Para manipulação e análise de dados.

* **NumPy:** Para operações numéricas.

* **Matplotlib:** Para visualização de dados.

* **Seaborn:** Para visualizações estatísticas e padronização de gráficos.

* **Jupyter Notebook:** Para o desenvolvimento interativo e apresentação da análise.

## Como Executar o Projeto

Como Executar o Projeto

1.Clone o Repositório:

git clone <URL_DO_SEU_REPOSITORIO>
cd <NOME_DO_SEU_REPOSITORIO>

2.Crie um Ambiente Virtual (Opcional, mas Recomendado):

python -m venv venv
source venv/bin/activate  # No Windows: .\venv\Scripts\activate

3.Instale as Dependências:

pip install pandas numpy matplotlib seaborn jupyter

4.Baixe o Dataset:
Certifique-se de que o arquivo ifood-restaurants-february-2021.csv esteja na mesma pasta do notebook. (Você pode precisar baixá-lo de uma fonte externa, se não estiver incluído no repositório).

5.Execute o Jupyter Notebook:

jupyter notebook case_est_descritiva.ipynb

Isso abrirá o notebook em seu navegador, onde você poderá executar as células e explorar a análise.

## Autor

Felipe Tamiozzo

Perfil no LinkedIn (www.linkedin.com/in/felipetamiozzo)

