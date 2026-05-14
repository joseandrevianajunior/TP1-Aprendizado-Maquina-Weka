### Relatório Final — Predição de Preços de Imóveis Comerciais com Weka

## Integrantes
- Dayane Rodrigues
- José André
- Helio Nogueira
- Luanna Benezar
- Lucas Marinho
- Marcos Gabriel

# Introdução

O mercado imobiliário comercial apresenta elevada complexidade na determinação de preços, devido à influência simultânea de fatores estruturais, econômicos e locacionais, nesse contexto, técnicas de aprendizado de máquina tornam-se ferramentas relevantes para modelar relações complexas e gerar estimativas preditivas mais precisas.

Este trabalho teve como objetivo construir e avaliar modelos de aprendizado de máquina capazes de prever o preço de imóveis comerciais utilizando a ferramenta Weka, o problema foi modelado como uma tarefa de regressão, uma vez que a variável alvo representa um valor numérico contínuo correspondente ao preço estimado do imóvel.

O domínio escolhido foi o mercado imobiliário comercial, no qual fatores como área construída, localização, fluxo de pessoas, idade do imóvel e padrão construtivo possuem influência direta na precificação.

---

# Definição do Problema

## Problema

Predição de preços de imóveis comerciais.

## Tipo de Problema

Regressão.

## Objetivo

Estimar o valor monetário de imóveis comerciais a partir de características estruturais e locacionais.

## Variáveis Utilizadas

### Entradas

- `area_m2`
- `bairro_valorizacao`
- `idade_imovel`
- `vagas_estacionamento`
- `distancia_centro_km`
- `fluxo_pessoas_dia`
- `taxa_vacancia_regiao`
- `tipo_imovel`
- `padrao_construtivo`
- `mes_cadastro`

### Saída

- `preco`

## Principais Desafios

- presença de ruído;
- existência de outliers;
- valores faltantes;
- relações não lineares entre atributos.

---

# Geração do Dataset

O dataset foi construído de forma sintética utilizando o ChatGPT Plus, com refinamento iterativo de prompts orientados ao domínio imobiliário.

A geração dos dados foi baseada em hipóteses realistas do mercado, incluindo:

- imóveis maiores tendem a possuir maior preço;
- regiões valorizadas aumentam o valor do imóvel;
- maior fluxo de pessoas favorece preços mais altos;
- imóveis mais distantes tendem a valer menos;
- imóveis antigos apresentam menor valorização.

Foram utilizados múltiplos prompts até atingir uma versão final capaz de gerar um dataset mais coerente e próximo de cenários reais.

O dataset final possui aproximadamente 700 instâncias contendo:

- atributos numéricos;
- atributos categóricos;
- valores faltantes;
- ruído;
- outliers;
- atributo irrelevante.

Além disso, foram inseridos propositalmente:

- ~5% de valores faltantes;
- ~8% de ruído;
- ~3% de outliers.

Essa estratégia teve como objetivo simular condições reais encontradas em aplicações de aprendizado de máquina.

---

# Prompts Utilizados

## Versão 1

```txt
Gere um dataset de imóveis comerciais com preço baseado em atributos.
Retorne apenas CSV.
```

## Versão 2

```txt
Gere um dataset com 700 imóveis comerciais contendo:
- area_m2
- bairro_valorizacao (baixo, medio, alto)
- idade_imovel
- distancia_centro_km
- fluxo_pessoas_dia
- preco

Os dados devem seguir lógica realista.
Retorne apenas CSV.
```

## Versão Final

```txt
Gere um dataset sintético com 700 imóveis comerciais.

Atributos:
- area_m2 (numérico)
- bairro_valorizacao (baixo, medio, alto)
- idade_imovel (numérico)
- vagas_estacionamento (numérico)
- distancia_centro_km (numérico)
- fluxo_pessoas_dia (numérico)
- taxa_vacancia_regiao (numérico)
- tipo_imovel (loja, sala_comercial, galpao, escritorio)
- padrao_construtivo (baixo, medio, alto)
- mes_cadastro (atributo irrelevante)
- preco (numérico)

Regras:
- maior área → maior preço
- melhor localização → maior preço
- maior fluxo → maior preço
- maior distância → menor preço
- imóveis antigos → menor preço

Inclua:
- 5% valores faltantes (?)
- 8% ruído
- 3% outliers

Retorne apenas CSV.
```

---

# Metodologia de Geração

O dataset utilizado neste trabalho foi construído de forma sintética utilizando um modelo de linguagem baseado em inteligência artificial, especificamente o ChatGPT Plus.

A geração dos dados foi realizada de maneira iterativa, com refinamento progressivo dos prompts, visando garantir coerência semântica, realismo e alinhamento com o domínio imobiliário comercial.

A construção do dataset não ocorreu de forma puramente aleatória. O processo foi orientado por hipóteses fundamentadas no comportamento real do mercado imobiliário.

## Hipóteses Utilizadas

- imóveis com maior área tendem a possuir maior valor;
- regiões mais valorizadas apresentam imóveis mais caros;
- maior fluxo de pessoas aumenta o potencial comercial do imóvel;
- imóveis mais distantes do centro tendem a possuir menor preço;
- imóveis mais antigos apresentam menor valorização;
- padrões construtivos superiores impactam positivamente o preço.

---

# Pré-processamento, Analize e Comparação do dataset

As informações utilizadas na análise exploratória foram obtidas a partir do dataset original, antes da aplicação das técnicas de pré-processamento, disponível no link de referência fornecido, assim como os procedimentos de filtragem, limpeza e pré-processamento aplicados ao conjunto de dados.

[Analize do Dataset](/preprocessamento/analise_inicial.md).
[Pré-Processamento](/preprocessamento/descricao_etapas.md).

As informações referentes à comparação entre o dataset original e o dataset pré-processado encontram-se disponíveis no link.

[Comparação dos Datasets](/preprocessamento/comparacacoDataset.md)

---

# Análise Exploratória dos Dados

## Análise dos Atributos Pré-processados no Weka

Atributos analisados:

```txt
area_m2
bairro_valorizacao
distancia_centro_km
extremeValue
fluxo_pessoas_dia
idade_imovel
outlier
padrao_construtivo
preco
taxa_vacancia_regiao
tipo_imovel
vagas_estacionamento
```

---

## 1. area_m2

![](/imagens/prints_weka/Atributos/weka_Atributos_proc/area_m2.png)

### Tipo
Numérico

### Análise

O atributo `area_m2` apresenta uma distribuição fortemente assimétrica à direita, indicando que a maior parte dos imóveis possui áreas pequenas ou médias, enquanto poucos imóveis apresentam áreas muito grandes.

A presença de uma cauda longa demonstra a existência de imóveis comerciais de grande porte, caracterizando outliers naturais do mercado imobiliário.

### Interpretação

Esse comportamento é coerente com cenários reais, onde existem muitos imóveis comuns e poucos imóveis extremamente amplos.

---

## 2. bairro_valorizacao

![](/imagens/prints_weka/Atributos/weka_Atributos_proc/bairro_valorizacao.png)

### Tipo
Categórico

### Categorias

```txt
baixo
medio
alto
```

### Análise

O atributo apresenta distribuição relativamente equilibrada entre as categorias, embora exista leve predominância de bairros classificados como `alto`.

### Interpretação

A valorização do bairro possui relação direta com o preço dos imóveis, sendo um fator fundamental no mercado imobiliário.

---

## 3. distancia_centro_km

![](/imagens/prints_weka/Atributos/weka_Atributos_proc/distancia_centro_km.png)

### Tipo
Numérico

### Análise

A distribuição do atributo apresenta comportamento próximo ao normal, com maior concentração em distâncias intermediárias.

Após o pré-processamento, os valores ficaram mais organizados e menos dispersos.

### Interpretação

A maioria dos imóveis está localizada em regiões moderadamente afastadas do centro urbano.

Existe tendência de redução do preço conforme aumenta a distância do centro.

---

## 4. fluxo_pessoas_dia

![](/imagens/prints_weka/Atributos/weka_Atributos_proc/fluxo_pessoas_dia.png)

### Tipo
Numérico

### Análise

O atributo apresenta forte concentração em valores menores e poucos casos extremos com fluxo muito elevado.

A distribuição possui cauda longa e assimetria positiva.

### Interpretação

A maioria dos imóveis está localizada em regiões de fluxo moderado, enquanto poucos imóveis estão em áreas altamente movimentadas.

---

## 5. idade_imovel

![](/imagens/prints_weka/Atributos/weka_Atributos_proc/idade_imovel.png)

### Tipo
Numérico

### Análise

A distribuição demonstra concentração de imóveis novos e intermediários, com poucos imóveis muito antigos.

Após o pré-processamento, os valores ficaram mais consistentes e organizados.

### Interpretação

O dataset representa predominantemente imóveis relativamente recentes.

---

## 6. taxa_vacancia_regiao

![](/imagens/prints_weka/Atributos/weka_Atributos_proc/taxa_vacancia_regiao.png)

### Tipo
Numérico

### Análise

A distribuição do atributo é relativamente equilibrada, com concentração em taxas médias de vacância.

### Interpretação

A maior parte das regiões possui vacância moderada, representando equilíbrio entre ocupação e disponibilidade de imóveis.

Regiões com alta vacância tendem a apresentar menor valorização imobiliária.

---

## 7. tipo_imovel

![](/imagens/prints_weka/Atributos/weka_Atributos_proc/tipo_imovel.png)

### Tipo
Categórico

### Categorias

```txt
loja
sala_comercial
escritorio
galpao
```

### Análise

A distribuição entre categorias está relativamente balanceada, embora `loja` apresente maior frequência e `galpao` menor quantidade de registros.

### Interpretação

Diferentes tipos de imóveis possuem padrões distintos de preço e valorização.

---

## 8. padrao_construtivo

![](/imagens/prints_weka/Atributos/weka_Atributos_proc/padrao_construtivo.png)

### Tipo
Categórico

### Categorias

```txt
baixo
medio
alto
```

### Análise

A categoria `medio` apresenta maior frequência no dataset, enquanto `alto` possui menor ocorrência.

### Interpretação

A maior parte dos imóveis possui padrão construtivo intermediário.

Imóveis de padrão elevado tendem a apresentar preços significativamente maiores.

---

## 9. vagas_estacionamento

![](/imagens/prints_weka/Atributos/weka_Atributos_proc/vagas_estacionamento.png)

### Tipo
Numérico

### Análise

O atributo apresenta forte concentração em baixos valores, indicando que a maioria dos imóveis possui poucas vagas de estacionamento.

Existem alguns casos extremos com grande quantidade de vagas.

### Interpretação

Imóveis comerciais maiores tendem a possuir mais vagas, aumentando seu valor de mercado.

---

## 10. preco

![](/imagens/prints_weka/Atributos/weka_Atributos_proc/preco.png)

### Tipo
Variável alvo (Target)

### Análise

A distribuição do preço apresenta forte assimetria positiva, característica comum em datasets imobiliários.

A maior parte dos imóveis possui preços moderados, enquanto poucos imóveis apresentam valores extremamente elevados.

### Interpretação

Esse comportamento representa adequadamente cenários reais do mercado imobiliário.

### Outliers

Existem preços muito elevados classificados como valores extremos.

---

## 11. Outlier

![](/imagens/prints_weka/Atributos/weka_Atributos_proc/outlier.png)


### Tipo
Binário

### Categorias

```txt
no
yes
```

### Análise

A maior parte das instâncias não foi classificada como outlier.

Aproximadamente 62 registros foram identificados como outliers.

---

### 12. ExtremeValue

![](/imagens/prints_weka/Atributos/weka_Atributos_proc/extremeValue.png)

### Tipo
Binário

### Categorias

```txt
no
yes
```

### Análise

Pouquíssimos registros foram classificados como valores extremos.

Apenas cerca de 11 instâncias apresentaram comportamento extremamente fora do padrão.

---

## Conclusão Geral

As visualizações confirmam que o pré-processamento realizado no Weka foi eficiente.

As etapas aplicadas contribuíram para:

- redução de ruído;
- tratamento de valores faltantes;
- melhor organização estatística;
- identificação de outliers;
- melhoria da distribuição dos dados.

Os atributos apresentam comportamentos coerentes com cenários reais do mercado imobiliário, tornando o dataset mais adequado para algoritmos de regressão.

Os atributos visualmente mais relevantes para previsão do preço são:

| Atributo | Importância Esperada |
|---|---|
| area_m2 | Muito Alta |
| bairro_valorizacao | Alta |
| fluxo_pessoas_dia | Alta |
| padrao_construtivo | Alta |
| distancia_centro_km | Média/Alta |
| tipo_imovel | Média/Alta |

Essas melhorias ajudam a justificar os bons resultados obtidos pelos modelos, principalmente:

- M5P
- RandomForest
- IBk

## Análise das Visualizações do Dataset Pré-processado

### Área × Preço

![](/imagens/visualizacoes/area_vs_preco.png)

Os pontos demonstram que:
- imóveis maiores tendem a possuir preços mais elevados;
- conforme a área aumenta, o preço cresce progressivamente;
- existem poucos imóveis extremamente grandes com preços muito altos.

Após o pré-processamento, os dados ficaram:
- menos dispersos;
- mais organizados;
- visualmente mais consistentes.

Foi observada uma relação positiva entre área e preço, indicando que imóveis maiores tendem a apresentar maior valor comercial.

### Distância × Preço

![](/imagens/visualizacoes/distancia_vs_preco.png)

O gráfico apresenta tendência negativa entre distância e preço.

Os dados mostram que:
- imóveis mais próximos do centro tendem a possuir maior valor;
- conforme a distância aumenta, o preço tende a diminuir.

Após o pré-processamento:
- a tendência ficou mais clara;
- os pontos ficaram menos dispersos;
- a relação estatística tornou-se mais evidente.

Observou-se uma relação inversa entre distância ao centro e preço, indicando que imóveis mais próximos do centro tendem a ser mais valorizados.

### Fluxo de Pessoas × Preço

![](/imagens/visualizacoes/fluxo_vs_preco.png)

O gráfico apresenta tendência positiva moderada.

Os dados indicam que:
- regiões com maior fluxo de pessoas possuem imóveis mais valorizados;
- existe dispersão moderada entre os pontos;
- alguns imóveis possuem fluxo muito alto.

Após o pré-processamento:
- os padrões ficaram mais claros;
- houve redução de ruído visual.

Regiões com maior fluxo de pessoas apresentaram maior concentração de imóveis com preços elevados.

### Bairro × Preço

![](/imagens/visualizacoes/bairro_vs_preco.png)

A valorização do bairro influencia diretamente o valor de mercado dos imóveis.

As categorias:
- `baixo`
- `medio`
- `alto`

apresentam separação relativamente clara após o pré-processamento.

Bairros classificados como “alto” apresentaram preços significativamente superiores em relação às demais categorias.

### Tipo do Imóvel × Preço

![](/imagens/visualizacoes/imovel_vs_preco.png)

O gráfico mostra diferenças significativas entre categorias de imóveis.

As categorias:
- loja;
- escritório;
- sala comercial;
- galpão;

apresentam faixas distintas de preço.

Após o pré-processamento:
- as categorias ficaram mais separadas;
- houve melhor organização visual dos dados.

Galpões apresentaram maior variabilidade de preços, enquanto salas comerciais e escritórios apresentaram maior concentração em faixas intermediárias.

---


# Modelagem e Avaliação

## Estratégia de Avaliação

Foi utilizada validação cruzada com 10 folds.

Essa estratégia foi escolhida devido:

- ao tamanho do dataset;
- à presença de ruído;
- à existência de outliers.

---

# Algoritmos Utilizados

## ZeroR

Modelo baseline utilizado como referência.

## IBk

Algoritmo baseado em distância.

Foram realizados testes com:

- K = 1
- K = 3
- K = 5
- K = 10

## RandomForest

Modelo baseado em múltiplas árvores de decisão.

Adequado para problemas não lineares e presença de ruído.

## M5P

Árvore de regressão combinada com modelos lineares locais.

## LinearRegression

Modelo linear utilizado para comparação.

## SMOreg

Modelo de regressão baseado em máquinas de vetor de suporte.

---

# Métricas Utilizadas

As seguintes métricas foram utilizadas:

- Correlation Coefficient
- MAE (Mean absolute error)
- RMSE (Root mean squared error)
- RAE (Relative absolute error)
- RRSE (Root relative squared error)

Quanto maior a correlação, melhor o modelo.

Para MAE, RMSE, RAE e RRSE, valores menores indicam melhor desempenho.

---

# Resultados Obtidos

| Algoritmo | Correlação | MAE | RMSE | RAE (%) | RRSE (%) |
|---|---|---|---|---|---|
| ZeroR | -0.1542 | 9819.69 | 15809.71 | 100.0000 | 100.0000 |
| IBk K=1 | 0.8555 | 4063.58 | 8195.54 | 41.3820 | 51.8387 |
| IBk K=3 | 0.8536 | 3755.55 | 8247.91 | 38.2452 | 52.1699 |
| IBk K=5 | 0.8464 | 3714.62 | 8469.64 | 37.8284 | 53.5724 |
| IBk K=10 | 0.8246 | 3843.06 | 9066.47 | 39.1363 | 57.3475 |
| M5P | 0.8966 | 2836.82 | 7021.53 | 28.9891 | 44.4128 |
| RandomForest | 0.8747 | 2614.48 | 7708.60 | 26.6249 | 48.7587 |
| SMOreg | 0.8128 | 3388.95 | 9262.24 | 34.5118 | 58.5858 |
| LinearRegression | 0.8413 | 4088.52 | 8538.93 | 41.6360 | 54.0107 |

---

# Discussão dos Resultados

A etapa de modelagem demonstrou que o problema de predição de preços de imóveis comerciais apresenta comportamento complexo, com influência simultânea de múltiplos atributos estruturais, econômicos e locacionais. Os resultados obtidos indicam que modelos capazes de capturar relações não lineares apresentaram desempenho superior em relação aos modelos estritamente lineares ou simplificados.

Além disso, a presença proposital de ruído, outliers e valores faltantes tornou o problema mais próximo de cenários reais encontrados em aplicações de aprendizado de máquina, permitindo uma avaliação mais robusta dos algoritmos.

---

# Análise Geral dos Resultados

Os experimentos mostraram que todos os modelos — com exceção do ZeroR — conseguiram aprender padrões relevantes do dataset. Isso demonstra que os atributos utilizados possuem efetivo poder preditivo sobre o preço dos imóveis comerciais.

Os melhores desempenhos foram obtidos por:

- M5P;
- RandomForest;
- IBk com valores intermediários de K.

Esses modelos possuem características importantes para problemas complexos:

- capacidade de modelar relações não lineares;
- tolerância a ruído;
- adaptação a interações entre variáveis;
- menor sensibilidade a distribuições não uniformes.

Por outro lado, modelos mais simples ou excessivamente generalistas apresentaram maior dificuldade para representar adequadamente o comportamento do dataset.

---

# ZeroR — Modelo Baseline

![](/imagens/prints_weka/Treino_Teste/test_01_zeroR.png)

O ZeroR foi utilizado como modelo de referência, ou seja, como baseline. Esse algoritmo não considera os atributos de entrada e realiza a previsão usando apenas um valor médio da variável alvo.

| Métrica | Valor |
|---|---|
| Correlation coefficient | -0.1542 |
| Mean absolute error | 9819.6923 |
| Root mean squared error | 15809.7109 |
| Relative absolute error | 100.0000 % |
| Root relative squared error | 100.0000 % |

O desempenho do ZeroR foi o pior entre todos os modelos avaliados. A correlação negativa indica que o modelo não conseguiu capturar nenhuma relação útil entre as características dos imóveis e seus preços. Isso era esperado, pois o ZeroR ignora completamente atributos como área, localização, fluxo de pessoas e padrão construtivo.

O erro absoluto médio de 9819.6923 e o RMSE de 15809.7109 demonstram que as previsões ficaram muito distantes dos valores reais. Como seus erros relativos foram de 100%, esse modelo serviu apenas como base de comparação. O fato de todos os outros algoritmos terem superado o ZeroR confirma que o dataset possui padrões relevantes e que os atributos selecionados contribuem para a predição do preço.

---

# IBk — Análise Detalhada do Ajuste de K

O algoritmo IBk foi testado utilizando múltiplos valores de K:

- K = 1
- K = 3
- K = 5
- K = 10

Essa etapa foi importante para avaliar o impacto do hiperparâmetro no desempenho do modelo.

---

# IBk — K = 1

![](/imagens/prints_weka/Treino_Teste/test_02_IBk_1.png)

O IBk com K = 1 utiliza apenas o vizinho mais próximo para realizar a predição. Isso torna o modelo altamente sensível aos exemplos individuais do dataset.

| Métrica | Valor |
|---|---|
| Correlation coefficient | 0.8555 |
| Mean absolute error | 4063.5859 |
| Root mean squared error | 8195.5452 |
| Relative absolute error | 41.3820 % |
| Root relative squared error | 51.8387 % |

O modelo apresentou uma correlação alta, indicando boa capacidade de aproximação entre valores reais e previstos. No entanto, o MAE ainda foi elevado quando comparado aos melhores modelos, como M5P e RandomForest.

Por usar apenas um vizinho, o K = 1 tende a se ajustar demais aos dados de treinamento. Isso pode causar overfitting, principalmente em um dataset com ruído e outliers. Assim, embora o desempenho tenha sido bom, o modelo pode ser instável em novos dados, pois uma única instância discrepante pode influenciar diretamente a previsão.

---

# IBk — K = 3

![](/imagens/prints_weka/Treino_Teste/test_03_IBk_3.png)

O IBk com K = 3 utiliza três vizinhos mais próximos para calcular a predição, reduzindo parcialmente a influência de valores isolados.

| Métrica | Valor |
|---|---|
| Correlation coefficient | 0.8536 |
| Mean absolute error | 3755.5576 |
| Root mean squared error | 8247.9159 |
| Relative absolute error | 38.2452 % |
| Root relative squared error | 52.1699 % |

Em comparação com K = 1, houve redução no erro absoluto médio, passando de 4063.5859 para 3755.5576. Isso indica que considerar mais vizinhos tornou o modelo mais estável.

Apesar da pequena queda na correlação, o modelo se tornou menos dependente de instâncias específicas. Esse resultado mostra que K = 3 teve melhor equilíbrio entre adaptação aos dados e capacidade de generalização.

---

# IBk — K = 5

![](/imagens/prints_weka/Treino_Teste/test_04_IBk_5.png) 

O IBk com K = 5 apresentou o melhor MAE entre as configurações testadas do IBk.

| Métrica | Valor |
|---|---|
| Correlation coefficient | 0.8464 |
| Mean absolute error | 3714.6290 |
| Root mean squared error | 8469.6421 |
| Relative absolute error | 37.8284 % |
| Root relative squared error | 53.5724 % |

Esse resultado indica que o uso de cinco vizinhos ajudou a suavizar o impacto de ruídos e pequenas variações nos dados. O MAE foi o menor entre os testes com IBk, mostrando que esse valor de K foi mais eficiente para reduzir o erro médio absoluto.

Entretanto, a correlação caiu em relação a K = 1 e K = 3, e o RMSE aumentou. Isso sugere que o modelo perdeu parte da capacidade de capturar variações locais específicas. Ainda assim, K = 5 apresentou um bom equilíbrio geral, sendo uma configuração mais estável do que K = 1.

---

# IBk — K = 10

![](/imagens/prints_weka/Treino_Teste/test_05_IBk_10.png)

O IBk com K = 10 utiliza dez vizinhos para realizar a previsão, tornando o modelo mais generalista.

| Métrica | Valor |
|---|---|
| Correlation coefficient | 0.8246 |
| Mean absolute error | 3843.0643 |
| Root mean squared error | 9066.4776 |
| Relative absolute error | 39.1363 % |
| Root relative squared error | 57.3475 % |

Com K = 10, o desempenho caiu em relação às configurações anteriores. A correlação foi a menor entre os testes do IBk, e o RMSE aumentou consideravelmente.

Esse comportamento indica que o modelo ficou suavizado demais. Ao considerar muitos vizinhos, ele perde sensibilidade para características específicas de cada imóvel. Assim, imóveis com comportamentos particulares podem receber previsões muito próximas da média local, reduzindo a precisão.

Portanto, os resultados indicam que valores intermediários de K foram mais adequados para este dataset.

---

# M5P — Melhor Desempenho Geral

![](/imagens/prints_weka/Treino_Teste/test_06_M5P.png)

[Codigo completo](/imagens/prints_weka/Treino_Teste/test_06_M5P.txt)

O M5P foi o modelo com melhor desempenho geral, principalmente por apresentar a maior correlação e o menor RMSE.

| Métrica | Valor |
|---|---|
| Correlation coefficient | 0.8966 |
| Mean absolute error | 2836.8241 |
| Root mean squared error | 7021.5333 |
| Relative absolute error | 28.9891 % |
| Root relative squared error | 44.4128 % |

A correlação de 0.8966 indica forte aproximação entre os valores previstos e os valores reais. Além disso, o RMSE de 7021.5333 foi o menor entre todos os modelos, mostrando que o M5P lidou melhor com erros maiores.

Esse desempenho é coerente com a natureza do problema, pois o preço de imóveis comerciais depende de combinações entre variáveis, como área, localização, fluxo de pessoas, distância ao centro e padrão construtivo.

O M5P combina árvores de decisão com modelos lineares locais, permitindo capturar relações não lineares e, ao mesmo tempo, ajustar modelos específicos para diferentes subconjuntos dos dados. Isso explica sua superioridade em relação à regressão linear simples.

De forma geral, o M5P foi o modelo mais adequado quando o foco é reduzir grandes erros de previsão e representar melhor a complexidade do problema.

---

# RandomForest — Robustez e Generalização

![](/imagens/prints_weka/Treino_Teste/test_07_randomFlorest.png)

O RandomForest apresentou excelente desempenho e obteve o menor erro absoluto médio entre todos os modelos.

| Métrica | Valor |
|---|---|
| Correlation coefficient | 0.8747 |
| Mean absolute error | 2614.4872 |
| Root mean squared error | 7708.6037 |
| Relative absolute error | 26.6249 % |
| Root relative squared error | 48.7587 % |

O principal destaque do RandomForest foi o MAE de 2614.4872, o menor entre todos os algoritmos avaliados. Isso significa que, em média, suas previsões ficaram mais próximas dos valores reais.

A correlação também foi alta, indicando boa capacidade preditiva. Porém, o RMSE foi maior que o do M5P, sugerindo que o RandomForest ainda apresentou alguns erros maiores em determinados casos.

Esse comportamento pode estar relacionado à presença de outliers. O RandomForest é robusto porque combina várias árvores de decisão, reduzindo a dependência de uma única estrutura. Por isso, ele lida bem com ruído e variações nos dados.

Assim, o RandomForest pode ser considerado o melhor modelo quando o objetivo principal é reduzir o erro médio das previsões, enquanto o M5P se destaca mais na redução de erros extremos.

---

# SMOreg — Desempenho Moderado

![](/imagens/prints_weka/Treino_Teste/test_08_SMOreg.png)

[Codigo completo](/imagens/prints_weka/Treino_Teste/test_06_M5P.txt)

O SMOreg é uma técnica baseada em máquinas de vetor de suporte aplicada a problemas de regressão.

| Métrica | Valor |
|---|---|
| Correlation coefficient | 0.8128 |
| Mean absolute error | 3388.9563 |
| Root mean squared error | 9262.2417 |
| Relative absolute error | 34.5118 % |
| Root relative squared error | 58.5858 % |

Apesar de ser um modelo mais sofisticado que a regressão linear, o SMOreg teve desempenho inferior ao M5P, RandomForest e algumas configurações do IBk.

A correlação de 0.8128 indica que o modelo conseguiu aprender parte dos padrões do dataset, mas o RMSE elevado mostra dificuldade em lidar com erros maiores. Isso pode ocorrer porque o SMOreg depende bastante da configuração de seus hiperparâmetros, como kernel, constante C e parâmetros de tolerância.

Sem uma calibração mais específica, o modelo pode não capturar adequadamente as relações não lineares presentes no dataset. Ainda assim, seu desempenho foi superior ao ZeroR, demonstrando que conseguiu extrair informações relevantes dos atributos.

---

# LinearRegression — Limitações do Modelo Linear

![](/imagens/prints_weka/Treino_Teste/test_09_linearRegression.png)

[Codigo completo](/imagens/prints_weka/Treino_Teste/test_09_linearRegression.txt)

A regressão linear foi utilizada para verificar se o problema poderia ser representado por uma relação linear global entre os atributos e o preço.

| Métrica | Valor |
|---|---|
| Correlation coefficient | 0.8413 |
| Mean absolute error | 4088.5223 |
| Root mean squared error | 8538.9330 |
| Relative absolute error | 41.6360 % |
| Root relative squared error | 54.0107 % |

O modelo apresentou desempenho razoável, com correlação de 0.8413. Isso indica que existe uma relação linear parcial entre os atributos e o preço dos imóveis.

Entretanto, o MAE e o RMSE foram mais altos que os dos modelos baseados em árvores, mostrando que a regressão linear não conseguiu representar toda a complexidade do problema.

Esse resultado confirma que o preço de imóveis comerciais não depende apenas de relações simples e diretas. Há interações importantes entre variáveis, como área, localização, fluxo de pessoas e tipo do imóvel.

Portanto, a regressão linear serviu como comparação útil, mas não foi o modelo mais adequado para este problema.

---

# Síntese Comparativa

De forma geral, os resultados mostram que os modelos superaram o baseline ZeroR, confirmando que os atributos possuem poder preditivo.

O M5P apresentou o melhor desempenho geral, com maior correlação e menor RMSE. Isso indica maior capacidade de capturar relações complexas e reduzir grandes erros.

O RandomForest apresentou o menor MAE, mostrando maior precisão média nas previsões.

O IBk teve desempenho satisfatório, principalmente com K = 3 e K = 5, mas mostrou sensibilidade à escolha do hiperparâmetro K.

O SMOreg apresentou desempenho intermediário e poderia melhorar com ajustes adicionais.

A regressão linear apresentou resultado razoável, mas inferior aos modelos não lineares, reforçando que o problema possui interações complexas entre variáveis.

---

# Impacto do Porcessamento

Os resultados demonstram que o pré-processamento teve papel fundamental no desempenho dos modelos.

A aplicação de:

- ReplaceMissingValues;
- Normalize;
- Remove;
- InterquartileRange;

contribuiu diretamente para:

- redução de inconsistências;
- melhoria na estabilidade;
- melhor adaptação dos algoritmos baseados em distância.

A normalização foi especialmente importante para o IBk, já que modelos baseados em distância são altamente sensíveis à escala dos atributos.

---

# Impacto dos Outliers

Os outliers influenciaram significativamente os resultados experimentais.

Isso ficou evidente principalmente na diferença entre:

- MAE;
- RMSE.

Como o RMSE penaliza erros maiores com mais intensidade, modelos mais sensíveis a valores extremos apresentaram maior degradação nessa métrica.

A decisão de manter os outliers mostrou-se metodologicamente adequada, pois permitiu avaliar:

- robustez;
- estabilidade;
- capacidade de generalização.

---

# Considerações Finais da Discussão

Os resultados experimentais confirmam que o problema de predição de preços imobiliários comerciais possui elevada complexidade e forte presença de relações não lineares.

Modelos baseados em árvores, especialmente:

- M5P;
- RandomForest;

demonstraram melhor capacidade de representar o comportamento do dataset.

Além disso, os experimentos evidenciaram:

- a importância do pré-processamento;
- o impacto dos hiperparâmetros;
- a influência dos outliers;
- a necessidade de modelos robustos para problemas reais.

De forma geral, os resultados obtidos foram coerentes com:

- as hipóteses de geração do dataset;
- o domínio imobiliário;
- a literatura relacionada à regressão de preços imobiliários.

---

# Conclusão

Os resultados obtidos demonstram que os atributos utilizados possuem forte poder preditivo para estimativa de preços de imóveis comerciais.

Os modelos baseados em árvores, especialmente M5P e RandomForest, apresentaram melhor desempenho, indicando que o problema possui relações complexas e não lineares entre variáveis.

O processo de pré-processamento mostrou-se fundamental para melhorar a qualidade dos dados e permitir maior robustez durante o treinamento dos modelos.

Além disso, o ajuste de hiperparâmetros realizado no IBk demonstrou a importância da parametrização adequada dos algoritmos.

Por fim, o trabalho evidenciou que técnicas de aprendizado de máquina podem ser aplicadas com sucesso em problemas de regressão imobiliária, especialmente quando combinadas com análise exploratória, pré-processamento adequado e avaliação experimental consistente.

---


# Referências

- HALL, Mark; FRANK, Eibe; HOLMES, Geoffrey; PFAHRINGER, Bernhard; REUTEMANN, Peter; WITTEN, Ian H. *The WEKA Data Mining Software: An Update*. SIGKDD Explorations, v. 11, n. 1, p. 10–18, 2009.

- OPENAI. *ChatGPT Plus*. Disponível em: <https://chat.openai.com/>.

- PARK, Byunghwa; BAE, Joonseok. *Using Machine Learning Algorithms for Housing Price Prediction: The Case of Fairfax County, Virginia Housing Data*. Expert Systems with Applications, v. 42, n. 6, p. 2928–2934, 2015.

- RAVIKUMAR, P. *Feature Selection Techniques in Machine Learning and Their Applications*. International Journal of Computer Applications, v. 160, n. 7, p. 23–28, 2017.

- CZARNOWSKI, Ireneusz. *Outlier Detection and Robust Regression in Real Estate Price Prediction*. Journal of Real Estate Analytics, v. 8, n. 2, p. 45–61, 2025.
