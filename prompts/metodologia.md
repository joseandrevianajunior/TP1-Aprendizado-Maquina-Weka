# Metodologia de Geração

O dataset utilizado neste trabalho foi construído de forma sintética utilizando um modelo de linguagem baseado em inteligência artificial, especificamente o ChatGPT Plus. A geração dos dados foi realizada de maneira iterativa, com refinamento progressivo dos prompts, visando garantir coerência semântica, realismo e alinhamento com o domínio imobiliário comercial.

## Fundamentação da Construção dos Dados

A geração dos dados foi baseada nas seguintes hipóteses do domínio:

- imóveis com maior área tendem a possuir maior valor;
- regiões mais valorizadas apresentam imóveis mais caros;
- maior fluxo de pessoas aumenta o potencial comercial do imóvel;
- imóveis mais distantes do centro tendem a possuir menor preço;
- imóveis mais antigos apresentam menor valorização;
- padrões construtivos superiores impactam positivamente o preço.

Essas relações foram incorporadas nos prompts utilizados durante a geração do dataset.

## Processo Iterativo de Geração

[Prompts](prompts_utilizados.txt)

A geração dos dados ocorreu em múltiplas etapas:

### Versão Inicial

[Versão 01](/prompts/versao01.csv)

Na primeira etapa, foi realizada uma geração genérica do dataset, contendo apenas atributos básicos e sem controle semântico detalhado.

### Versão Intermediária

[Versão 02](/prompts/versao02.csv)

Na segunda versão, foram adicionados novos atributos relevantes para o domínio imobiliário, além de regras básicas de coerência entre variáveis.

### Versão Final

[Versão 03](/prompts/versao03.csv)

Na versão final, o dataset passou a incluir:

- regras explícitas de relacionamento entre atributos;
- inserção controlada de ruído;
- inclusão de outliers;
- valores faltantes;
- atributo irrelevante para avaliação de pré-processamento.

Essa abordagem permitiu gerar um conjunto de dados mais próximo de cenários reais encontrados em problemas de aprendizado de máquina.

## Características do Dataset

O dataset final possui aproximadamente 700 instâncias contendo atributos numéricos e categóricos relacionados ao mercado imobiliário comercial.

Os principais atributos utilizados foram:

- area_m2
- bairro_valorizacao
- idade_imovel
- vagas_estacionamento
- distancia_centro_km
- fluxo_pessoas_dia
- taxa_vacancia_regiao
- tipo_imovel
- padrao_construtivo
- mes_cadastro
- preco

Além disso, foram inseridos propositalmente:

- aproximadamente 5% de valores faltantes;
- aproximadamente 8% de ruído;
- aproximadamente 3% de outliers.

A inclusão dessas imperfeições teve como objetivo simular cenários mais realistas e permitir avaliação da robustez dos algoritmos utilizados.

## Controle de Qualidade dos Dados

Após a geração inicial, o dataset passou por uma etapa de validação exploratória para verificar:

- coerência entre atributos;
- distribuição dos valores;
- presença de inconsistências;
- plausibilidade das relações entre variáveis.

Essa etapa foi fundamental para garantir maior qualidade e consistência dos dados antes da aplicação das técnicas de pré-processamento e modelagem.

## Conversão para ARFF

Por fim, o dataset foi convertido para o formato `.arff`, compatível com a ferramenta Weka, permitindo sua utilização nas etapas de análise exploratória, pré-processamento, treinamento e avaliação dos modelos de aprendizado de máquina.
