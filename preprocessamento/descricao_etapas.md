# Descrição das Etapas de Pré-processamento

## Objetivo do Pré-processamento

A etapa de pré-processamento foi realizada com o objetivo de preparar o dataset para a modelagem no Weka, reduzindo inconsistências, melhorando a qualidade dos dados e minimizando possíveis impactos negativos causados por ruído, diferenças de escala e atributos irrelevantes.

As decisões adotadas durante o pré-processamento foram fundamentadas na análise exploratória inicial do dataset, permitindo que o tratamento dos dados fosse realizado de forma orientada por evidências e alinhada às características do problema.

O pré-processamento foi executado utilizando filtros da ferramenta Weka.

---

# Etapa 1 — Tratamento de Valores Faltantes

## Problema Identificado

Durante a análise exploratória foram identificados valores ausentes representados pelo símbolo `?` em diferentes atributos do dataset.

A presença de valores faltantes pode comprometer o treinamento dos modelos, especialmente algoritmos que não conseguem lidar diretamente com dados incompletos.

Além disso, a remoção de instâncias contendo valores ausentes reduziria o volume total de dados disponíveis para treinamento e avaliação.

---

## Filtro Utilizado

```txt
unsupervised → attribute → ReplaceMissingValues
```

---

## Funcionamento do Filtro

O filtro `ReplaceMissingValues` realiza imputação automática dos valores ausentes:

* atributos numéricos → substituição pela média;
* atributos categóricos → substituição pela moda.

Esse processo permite preservar todas as instâncias do dataset sem descartar informações relevantes.

---

## Justificativa da Escolha

A utilização do filtro foi considerada adequada porque:

* mantém o volume original de dados;
* reduz impacto de instâncias incompletas;
* melhora a compatibilidade com algoritmos de regressão;
* evita perda excessiva de informação.
---

# Etapa 2 — Remoção de Atributos Irrelevantes

## Problema Identificado

A análise exploratória indicou que o atributo `mes_cadastro` não apresentava relação significativa com a variável alvo `preco`.

O atributo possuía distribuição uniforme e não demonstrava impacto relevante na valorização dos imóveis comerciais.

A permanência desse atributo poderia introduzir ruído desnecessário no treinamento dos modelos.

---

## Filtro Utilizado

```txt
unsupervised → attribute → Remove
```

---

## Funcionamento do Filtro

O filtro `Remove` permite excluir atributos específicos do dataset.

Nesse caso, o atributo removido foi:

```txt
mes_cadastro
```

---

## Justificativa da Escolha

A remoção de atributos irrelevantes contribui para:

* reduzir ruído nos dados;
* simplificar o processo de aprendizado;
* melhorar a capacidade de generalização dos modelos;
* diminuir complexidade desnecessária.

Além disso, atributos sem relevância estatística podem prejudicar algoritmos mais sensíveis à dimensionalidade.

---

# Etapa 3 — Normalização dos Dados

## Problema Identificado

Foi observado que os atributos numéricos apresentavam escalas muito diferentes.

Exemplos:

* área do imóvel em metros quadrados;
* distância ao centro em quilômetros;
* fluxo de pessoas em centenas ou milhares;
* preço em valores monetários elevados.

Diferenças de escala podem impactar negativamente algoritmos baseados em distância, como o IBk (KNN).

---

## Filtro Utilizado

```txt
unsupervised → attribute → Normalize
```

---

## Funcionamento do Filtro

O filtro `Normalize` transforma os atributos numéricos para uma escala padronizada, geralmente entre 0 e 1.

Isso impede que atributos com valores maiores dominem o treinamento do modelo.

---

## Justificativa da Escolha

A normalização foi aplicada porque:

* melhora estabilidade dos algoritmos;
* reduz impacto de diferenças de escala;
* melhora desempenho de modelos baseados em distância;
* facilita convergência de determinados algoritmos.

Essa etapa foi especialmente importante para os experimentos com o algoritmo IBk.

---

# Etapa 4 — Avaliação de Outliers

## Problema Identificado

Durante a análise exploratória foram identificados valores extremos principalmente nos atributos:

* `preco`;
* `area_m2`;
* `fluxo_pessoas_dia`.

Esses valores representam imóveis significativamente diferentes da maior parte das instâncias do dataset.

Outliers podem afetar modelos lineares e aumentar erros de predição.

---

## Filtro Utilizado

```txt
unsupervised → attribute → InterquartileRange
```

---

## Funcionamento do Filtro

O filtro `InterquartileRange` identifica instâncias discrepantes utilizando o intervalo interquartil (IQR).

A técnica analisa:

* quartil inferior (Q1);
* quartil superior (Q3);
* amplitude interquartil.

Instâncias muito distantes desse intervalo são marcadas como possíveis outliers.

---

## Justificativa da Escolha

O uso do filtro permitiu:

* identificar sistematicamente valores extremos;
* analisar comportamento dos dados;
* avaliar robustez dos modelos.

Os outliers não foram removidos, pois representam cenários plausíveis do mercado imobiliário comercial.

Imóveis muito grandes, localizações privilegiadas e construções de alto padrão podem naturalmente gerar valores extremos.

Além disso, manter os outliers permitiu avaliar a capacidade dos algoritmos em lidar com dados ruidosos.

---

# Impacto do Pré-processamento

Após a aplicação das etapas de pré-processamento, o dataset apresentou melhorias significativas em relação à consistência e qualidade dos dados.

Os principais resultados obtidos foram:

* eliminação de valores faltantes;
* remoção de atributo irrelevante;
* padronização de escalas numéricas;
* identificação estruturada de outliers;
* maior compatibilidade com algoritmos de regressão.

Essas transformações contribuíram diretamente para melhorar a qualidade da etapa de modelagem e tornar os experimentos mais confiáveis.

---

# Conclusão

O pré-processamento desempenhou papel fundamental na preparação do dataset para os experimentos de aprendizado de máquina.

As decisões adotadas foram fundamentadas na análise exploratória inicial e buscaram equilibrar:

* preservação das informações;
* redução de ruído;
* melhoria da qualidade dos dados;
* manutenção da coerência com o domínio imobiliário.

Além disso, as etapas aplicadas contribuíram para aumentar a robustez dos modelos e melhorar a interpretação dos resultados obtidos durante a fase de modelagem.
