# Análise Exploratória Inicial do Dataset

## Objetivo da Análise

Antes da aplicação das técnicas de pré-processamento, foi realizada uma análise exploratória inicial com o objetivo de compreender o comportamento geral do dataset, identificar inconsistências, detectar padrões e levantar hipóteses sobre possíveis dificuldades para a etapa de modelagem.

Essa etapa é fundamental para garantir que o pré-processamento seja realizado de forma orientada por evidências, permitindo decisões mais coerentes sobre tratamento de dados, escolha de algoritmos e interpretação dos resultados.

Além disso, a análise exploratória auxilia na identificação de relações entre atributos e na compreensão da complexidade do problema de regressão proposto.

---

# Visão Geral do Dataset

O dataset utilizado representa imóveis comerciais com diferentes características físicas, econômicas e locacionais. O conjunto possui aproximadamente 700 instâncias e foi construído sinteticamente com base em hipóteses realistas do mercado imobiliário.

Os atributos presentes no dataset incluem:

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
- `preco`

O atributo `preco` foi definido como variável alvo do problema, caracterizando uma tarefa de regressão.

---

# Análise Individual dos Atributos

## Área do Imóvel (`area_m2`)

![](/imagens/prints_weka/Atributos/weka_Atributos_nao_proc/area_m2.png)

A distribuição do atributo `area_m2` apresentou concentração significativa em imóveis de pequeno e médio porte, enquanto uma parcela menor do dataset contém imóveis com áreas elevadas.

Foi observada:

- assimetria leve à direita;
- presença de valores extremos;
- maior densidade em áreas intermediárias.

A existência de imóveis muito grandes aumenta a dispersão dos dados e pode impactar modelos sensíveis à escala, especialmente algoritmos lineares e baseados em distância.

Além disso, a área mostrou forte relação com o preço do imóvel, indicando alto poder preditivo.

---

## Valorização do Bairro (`bairro_valorizacao`)

![](/imagens/prints_weka/Atributos/weka_Atributos_nao_proc/bairro_valorizacao.png)

O atributo categórico apresentou distribuição relativamente equilibrada entre as categorias:

- baixo;
- medio;
- alto.

A análise mostrou que regiões mais valorizadas concentram imóveis com preços mais elevados, enquanto bairros classificados como "baixo" apresentam predominância de imóveis mais baratos.

Esse comportamento demonstra coerência com o domínio imobiliário e reforça a importância da localização na composição do preço.

---

## Idade do Imóvel (`idade_imovel`)

![](/imagens/prints_weka/Atributos/weka_Atributos_nao_proc/idade_imovel.png)

A variável `idade_imovel` apresentou ampla variação entre imóveis novos e antigos.

Observou-se:

- dispersão relativamente alta;
- presença de imóveis muito antigos;
- concentração moderada em imóveis de idade intermediária.

Foi identificada tendência de desvalorização associada ao aumento da idade do imóvel, embora essa relação não seja perfeitamente linear.

---

## Número de Vagas (`vagas_estacionamento`)

![](/imagens/prints_weka/Atributos/weka_Atributos_nao_proc/vagas_estacionamento.png)

O atributo apresentou distribuição discreta, com predominância de imóveis contendo entre 0 e 3 vagas.

Poucas instâncias apresentaram valores muito elevados de vagas de estacionamento.

A análise sugere influência positiva sobre o preço, porém com impacto menor quando comparado a atributos como localização e área.

---

## Distância ao Centro (`distancia_centro_km`)

![](/imagens/prints_weka/Atributos/weka_Atributos_nao_proc/distancia_centro_km.png)

A distribuição revelou predominância de imóveis próximos ao centro urbano, além da existência de algumas instâncias mais distantes.

Foi observada:

- concentração em valores baixos;
- relação inversa entre distância e preço;
- dispersão moderada.

Imóveis localizados próximos a regiões centrais tendem a apresentar maior valorização comercial devido ao maior fluxo econômico e facilidade de acesso.

---

## Fluxo de Pessoas (`fluxo_pessoas_dia`)

![](/imagens/prints_weka/Atributos/weka_Atributos_nao_proc/fluxo_pessoas_dia.png)

O atributo `fluxo_pessoas_dia` apresentou grande variabilidade entre as instâncias.

A análise revelou:

- regiões com baixa movimentação;
- regiões altamente comerciais;
- dispersão significativa.

Foi observada correlação positiva entre fluxo de pessoas e preço do imóvel, indicando que regiões mais movimentadas tendem a possuir maior potencial econômico.

Entretanto, a dispersão dos pontos sugere que o fluxo não atua isoladamente, dependendo também de atributos como localização, área e padrão construtivo.

---

## Taxa de Vacância (`taxa_vacancia_regiao`)

![](/imagens/prints_weka/Atributos/weka_Atributos_nao_proc/taxa_vacancia_regiao.png)

A taxa de vacância apresentou diferentes níveis ao longo do dataset.

Regiões com alta vacância tendem a apresentar menor valorização comercial, indicando possível relação negativa com o preço dos imóveis.

Esse comportamento está alinhado ao contexto econômico do problema.

---

## Tipo do Imóvel (`tipo_imovel`)

![](/imagens/prints_weka/Atributos/weka_Atributos_nao_proc/tipo_imovel.png)

Foram identificadas diferentes categorias de imóveis comerciais:

- loja;
- sala_comercial;
- galpao;
- escritorio.

Os galpões apresentaram maior dispersão de preços e concentraram alguns dos maiores valores do dataset, provavelmente devido às maiores áreas construídas.

Já salas comerciais e escritórios apresentaram maior concentração em faixas intermediárias de preço.

Isso demonstra que diferentes categorias possuem comportamentos distintos de valorização.

---

## Padrão Construtivo (`padrao_construtivo`)

![](/imagens/prints_weka/Atributos/weka_Atributos_nao_proc/padrao_construrivo.png)

O atributo apresentou distribuição entre os níveis:

- baixo;
- medio;
- alto.

Imóveis classificados com padrão construtivo elevado apresentaram tendência de maior valorização, reforçando a relevância desse atributo para o problema.

---

## Mês de Cadastro (`mes_cadastro`)

![](/imagens/prints_weka/Atributos/weka_Atributos_nao_proc/mes_cadastro.png)

O atributo apresentou distribuição uniforme ao longo dos meses.

Não foram observados padrões relevantes entre o mês de cadastro e o preço dos imóveis.

Dessa forma, o atributo foi considerado irrelevante para a modelagem.

---

## Variável Alvo (`preco`)

![](/imagens/prints_weka/Atributos/weka_Atributos_nao_proc/preco.png)

A distribuição do atributo `preco` apresentou:

- assimetria à direita;
- grande variabilidade;
- presença de valores extremos.

A existência de imóveis com preços muito elevados indica presença de outliers e aumenta a complexidade do problema de regressão.

Além disso, a dispersão observada sugere que o preço depende da interação simultânea entre múltiplos atributos.

---

# Análise das Relações Entre Variáveis

## Área × Preço

![](/imagens/visualizacoes/area_vs_preco_np.png)

A visualização entre `area_m2` e `preco` mostrou tendência positiva clara.

Imóveis maiores tendem a apresentar preços mais elevados. Entretanto, a presença de pontos muito dispersos demonstra que a área não é suficiente para explicar o preço isoladamente.

Também foram identificados outliers com preços extremamente altos.

---

## Distância × Preço

![](/imagens/visualizacoes/distancia_vs_preco_np.png)

A relação entre `distancia_centro_km` e `preco` apresentou comportamento inverso.

Imóveis mais próximos do centro concentram maiores valores, enquanto imóveis mais afastados tendem a apresentar preços menores.

Apesar disso, alguns imóveis distantes ainda apresentaram preços elevados, indicando interação com outros atributos relevantes.

---

## Fluxo de Pessoas × Preço

![](/imagens/visualizacoes/fluxo_vs_preco_np.png)

Foi observada relação positiva entre `fluxo_pessoas_dia` e `preco`.

Regiões com maior circulação comercial tendem a apresentar imóveis mais valorizados.

Entretanto, a dispersão observada indica comportamento parcialmente não linear.

---

## Valorização da Região × Preço

![](/imagens/visualizacoes/bairro_vs_preco_np.png)

A análise demonstrou separação clara entre as categorias de valorização do bairro.

Imóveis localizados em regiões classificadas como "alto" concentraram os maiores preços do dataset.

Isso evidencia forte poder explicativo do atributo.

---

## Tipo de Imóvel × Preço

![](/imagens/visualizacoes/imovel_vs_preco_np.png)

A visualização revelou diferenças significativas entre os tipos de imóveis.

Galpões apresentaram maior amplitude de preços, enquanto salas comerciais e escritórios concentraram valores intermediários.

Esse comportamento reforça a necessidade de modelos capazes de capturar interações complexas entre atributos.

---

# Problemas Identificados

Durante a análise exploratória foram identificados diversos problemas típicos de cenários reais:

- valores faltantes representados por "?";
- presença de ruído;
- outliers em atributos numéricos;
- diferenças de escala;
- atributo irrelevante;
- relações não lineares;
- interações entre variáveis.

Esses fatores aumentam a complexidade do problema e justificam a necessidade de pré-processamento antes da etapa de modelagem.

---

# Hipóteses Levantadas

Com base na análise realizada, foram levantadas as seguintes hipóteses:

- algoritmos lineares podem apresentar desempenho limitado;
- modelos baseados em árvores podem lidar melhor com relações complexas;
- normalização será importante para algoritmos baseados em distância;
- outliers podem impactar significativamente determinados modelos;
- atributos irrelevantes devem ser removidos;
- o problema possui comportamento parcialmente não linear.

---

# Conclusão da Análise Exploratória

A análise exploratória mostrou que o dataset apresenta comportamento coerente com o domínio imobiliário comercial, contendo relações plausíveis entre os atributos e a variável alvo.

As visualizações confirmaram tendências esperadas, como:

- imóveis maiores tendendo a possuir maior preço;
- regiões valorizadas apresentando imóveis mais caros;
- maior fluxo comercial aumentando o valor dos imóveis;
- imóveis próximos ao centro apresentando maior valorização.

Também foram identificadas características que aumentam a complexidade do problema, incluindo presença de ruído, valores faltantes, outliers e relações não lineares.

Essas observações foram fundamentais para orientar as etapas posteriores de pré-processamento e modelagem.
