# Predição de Preços de Imóveis Comerciais com Weka

## Sobre o Repositório

Este repositório contém o desenvolvimento completo do Trabalho Prático 1 da disciplina de Inteligência Artificial, utilizando a ferramenta Weka para construção, análise e avaliação de modelos de regressão aplicados à predição de preços de imóveis comerciais.

O projeto foi organizado de forma reprodutível e estruturada, permitindo compreender todas as etapas do pipeline de aprendizado de máquina, desde a geração do dataset até a interpretação final dos resultados experimentais.

O repositório inclui:

* datasets originais e preprocessados;
* prompts utilizados na geração dos dados;
* análises exploratórias;
* visualizações gráficas;
* resultados dos algoritmos;
* relatórios em Markdown;
* prints do Weka;
* documentação completa do projeto.

---

## Objetivo do Projeto

O objetivo principal deste trabalho foi aplicar técnicas de aprendizado de máquina para prever preços de imóveis comerciais utilizando atributos estruturais e locacionais.

O problema foi tratado como uma tarefa de regressão, na qual o modelo deve estimar um valor numérico contínuo correspondente ao preço do imóvel.

---

## Tema do Projeto

Predição de preços de imóveis comerciais utilizando aprendizado de máquina.

---

## Problema Abordado

O mercado imobiliário comercial apresenta elevada complexidade devido à influência simultânea de diversos fatores como:

* área construída;
* localização;
* fluxo de pessoas;
* padrão construtivo;
* idade do imóvel;
* distância ao centro urbano.

Além disso, problemas reais de dados também foram simulados no dataset, incluindo:

* ruído;
* outliers;
* valores faltantes;
* atributos irrelevantes.

---

## Organização do Repositório

```txt
TP1_Aprendizado_Maquina_Weka-main/
│
├── README.md
│
├── datasets/
│   ├── dataset_original.arff
│   └── dataset_preprocessado.arff
│
├── prompts/
│   ├── metodologia.md
│   ├── prompts_utilizados.txt
│   ├── versao01.csv
│   ├── versao02.csv
│   └── versao03.csv
│
├── preprocessamento/
│   ├── analise_inicial.md
│   └── descricao_etapas.md
│
├── relatorio/
│   └── relatorio_final.md
│
└── imagens/
    ├── pipeline_geracao.png
    ├── visualizacoes/
    └── prints_weka/
        ├── atributos/
        └── treino_teste/
```

---

## Dataset

### Construção do Dataset

O dataset foi construído de forma sintética utilizando o ChatGPT Plus com refinamento iterativo de prompts.

A geração foi baseada em hipóteses realistas do mercado imobiliário comercial.

### Quantidade de Instâncias

```txt
700 instâncias
```

### Características do Dataset

O dataset contém:

* atributos numéricos;
* atributos categóricos;
* ruído;
* valores faltantes;
* outliers;
* atributos irrelevantes.

---

## Atributos Utilizados

### Variáveis de Entrada

| Atributo             | Tipo        |
| -------------------- | ----------- |
| area_m2              | Numérico    |
| bairro_valorizacao   | Categórico  |
| idade_imovel         | Numérico    |
| vagas_estacionamento | Numérico    |
| distancia_centro_km  | Numérico    |
| fluxo_pessoas_dia    | Numérico    |
| taxa_vacancia_regiao | Numérico    |
| tipo_imovel          | Categórico  |
| padrao_construtivo   | Categórico  |
| mes_cadastro         | Irrelevante |

### Variável Alvo

| Atributo | Tipo     |
| -------- | -------- |
| preco    | Numérico |

---

## Pré-processamento dos Dados

O pré-processamento foi realizado utilizando filtros do Weka.

### Técnicas Aplicadas

| Técnica              | Objetivo                        |
| -------------------- | ------------------------------- |
| ReplaceMissingValues | Tratamento de valores faltantes |
| Remove               | Remoção de atributo irrelevante |
| Normalize            | Normalização dos atributos      |
| InterquartileRange   | Identificação de outliers       |

### Principais Melhorias

Após o pré-processamento, observou-se:

* redução de ruído;
* remoção de inconsistências;
* ausência de valores faltantes;
* melhor organização estatística;
* melhor qualidade para regressão.

---

## Análise Exploratória

Foram realizadas análises estatísticas e visuais para compreender o comportamento dos atributos.

### Principais Relações Encontradas

| Relação                | Comportamento           |
| ---------------------- | ----------------------- |
| Área × Preço           | Positiva                |
| Bairro × Preço         | Positiva                |
| Distância × Preço      | Negativa                |
| Fluxo × Preço          | Positiva                |
| Tipo do imóvel × Preço | Dependente da categoria |

---

## Algoritmos Utilizados

Os seguintes algoritmos foram avaliados:

* ZeroR;
* IBk;
* RandomForest;
* M5P;
* LinearRegression;
* SMOreg.

---

## Ajuste de Hiperparâmetros

No algoritmo IBk foram realizados testes utilizando diferentes valores de K:

```txt
K = 1
K = 3
K = 5
K = 10
```

Essa etapa permitiu avaliar o impacto da parametrização no desempenho do modelo.

---

## Estratégia de Avaliação

Foi utilizada validação cruzada com 10 folds.

Essa estratégia foi escolhida devido:

* ao tamanho do dataset;
* à presença de ruído;
* à existência de outliers.

---

## Métricas Utilizadas

As seguintes métricas foram utilizadas:

* Correlation Coefficient;
* Mean Absolute Error (MAE);
* Root Mean Squared Error (RMSE);
* Relative Absolute Error (RAE);
* Root Relative Squared Error (RRSE).

---

## Resultados Obtidos

| Algoritmo        | Correlação | MAE     | RMSE     |
| ---------------- | ---------- | ------- | -------- |
| ZeroR            | -0.1542    | 9819.69 | 15809.71 |
| IBk K=1          | 0.8555     | 4063.58 | 8195.54  |
| IBk K=3          | 0.8536     | 3755.55 | 8247.91  |
| IBk K=5          | 0.8464     | 3714.62 | 8469.64  |
| IBk K=10         | 0.8246     | 3843.06 | 9066.47  |
| M5P              | 0.8966     | 2836.82 | 7021.53  |
| RandomForest     | 0.8747     | 2614.48 | 7708.60  |
| SMOreg           | 0.8128     | 3388.95 | 9262.24  |
| LinearRegression | 0.8413     | 4088.52 | 8538.93  |

---

## Melhor Modelo

O algoritmo M5P apresentou o melhor desempenho geral.

### Principais Destaques

* maior correlação;
* menor RMSE;
* melhor adaptação a relações não lineares.

O RandomForest também apresentou excelente desempenho, obtendo o menor MAE.

---

## Resultados Visuais

O repositório contém:

* histogramas dos atributos;
* gráficos de dispersão;
* comparação entre datasets;
* visualizações antes e depois do pré-processamento;
* prints completos do Weka;
* análises gráficas dos modelos.

---

## Tecnologias Utilizadas

| Ferramenta   | Função                        |
| ------------ | ----------------------------- |
| Weka         | Modelagem e pré-processamento |
| ChatGPT Plus | Geração do dataset            |
| Markdown     | Documentação                  |
| GitHub       | Organização e versionamento   |

---

## Como Executar o Projeto

### 1. Instalar o Weka

Download oficial:

```txt
https://www.cs.waikato.ac.nz/ml/weka/
```

### 2. Abrir o Dataset

```txt
Explorer → Open File → dataset_preprocessado.arff
```

### 3. Executar os Algoritmos

```txt
Classify → Escolher algoritmo → Start
```

### 4. Estratégia de Avaliação

Selecionar:

```txt
Cross-validation → 10 folds
```

---

## Principais Conclusões

Os experimentos demonstraram que:

* os atributos utilizados possuem forte poder preditivo;
* o pré-processamento teve impacto direto no desempenho;
* modelos baseados em árvores apresentaram melhores resultados;
* relações não lineares possuem forte influência no problema;
* o ajuste de hiperparâmetros altera significativamente os resultados.

Além disso, o trabalho evidenciou a importância:

* da análise exploratória;
* da interpretação crítica dos resultados;
* da organização do pipeline de ciência de dados;
* da documentação reprodutível no GitHub.

---

## Considerações Finais

Este projeto permitiu aplicar de forma prática conceitos fundamentais de aprendizado de máquina utilizando o Weka.

O trabalho envolveu todas as etapas de um pipeline de mineração de dados, incluindo:

* geração de dados;
* análise exploratória;
* pré-processamento;
* treinamento;
* avaliação;
* interpretação de resultados.

Os resultados obtidos demonstraram que técnicas de aprendizado de máquina podem ser utilizadas com eficiência para problemas de regressão imobiliária, especialmente quando combinadas com pré-processamento adequado e modelos robustos.

---

## Integrantes

* Dayane Rodrigues
* José André
* Helio Nogueira
* Luanna Benezar
* Lucas Marinho
* Marcos Gabriel

---

## Referências

* HALL, Mark; FRANK, Eibe; HOLMES, Geoffrey; PFAHRINGER, Bernhard; REUTEMANN, Peter; WITTEN, Ian H. *The WEKA Data Mining Software: An Update*. SIGKDD Explorations, v. 11, n. 1, p. 10–18, 2009.

* OPENAI. *ChatGPT Plus*. Disponível em: https://chat.openai.com/.

* PARK, Byunghwa; BAE, Joonseok. *Using Machine Learning Algorithms for Housing Price Prediction: The Case of Fairfax County, Virginia Housing Data*. Expert Systems with Applications, v. 42, n. 6, p. 2928–2934, 2015.

* RAVIKUMAR, P. *Feature Selection Techniques in Machine Learning and Their Applications*. International Journal of Computer Applications, v. 160, n. 7, p. 23–28, 2017.

* CZARNOWSKI, Ireneusz. *Outlier Detection and Robust Regression in Real Estate Price Prediction*. Journal of Real Estate Analytics, v. 8, n. 2, p. 45–61, 2025.
