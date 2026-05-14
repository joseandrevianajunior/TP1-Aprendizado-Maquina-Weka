# Comparação entre o Dataset Original e o Dataset Pré-Processado

![](/imagens/prints_weka/Atributos/datassetnaoprecessado_datassetpreprocessado_2.png)

A comparação entre o dataset original e o dataset pré-processado evidencia melhorias significativas na qualidade e organização dos dados, principalmente no atributo `area_m2`.

## Dataset Original

No dataset original, o atributo `area_m2` apresentava:

- 30 valores ausentes (4%);
- Valores variando entre **17.98 m²** e **3091.05 m²**;
- Média de **205.43**;
- Desvio padrão de **312.646**.

Esses dados demonstram uma elevada dispersão, causada principalmente pela presença de imóveis extremamente grandes. Esse comportamento pode impactar negativamente algoritmos sensíveis à escala e a valores extremos, especialmente modelos lineares e baseados em distância.

Além disso, a presença de dados ausentes poderia comprometer a qualidade da modelagem e a confiabilidade dos resultados obtidos.

---

## Dataset Pré-Processado

Após a aplicação das técnicas de pré-processamento, o dataset apresentou melhorias importantes:

- Remoção completa dos valores ausentes;
- Normalização dos valores do atributo `area_m2`;
- Valores ajustados para a faixa entre **0 e 1**;
- Média reduzida para **0.061**;
- Desvio padrão reduzido para **0.1**.

A normalização reduziu significativamente a dispersão dos dados, tornando os atributos mais equilibrados e adequados para algoritmos de aprendizado de máquina.

Outro ponto importante foi a criação dos atributos:

- `Outlier`
- `ExtremeValue`

Esses atributos auxiliam na identificação e controle de registros extremos, permitindo uma análise mais robusta e confiável do conjunto de dados.

---

## Análise Comparativa

A comparação entre os dois datasets demonstra que o pré-processamento contribuiu diretamente para a melhoria da qualidade dos dados.

Enquanto o dataset original apresentava alta dispersão, valores extremos e dados ausentes, o dataset pré-processado tornou-se mais padronizado, organizado e adequado para a etapa de modelagem.

As principais melhorias observadas foram:

| Característica | Dataset Original | Dataset Pré-Processado |
|---|---|---|
| Valores ausentes | 30 (4%) | 0 |
| Escala dos dados | 17.98 até 3091.05 | 0 até 1 |
| Dispersão | Muito alta | Reduzida |
| Presença de outliers | Elevada | Controlada |
| Padronização | Não aplicada | Aplicada |
| Qualidade para modelagem | Moderada | Alta |

---

## Considerações

De forma geral, o pré-processamento tornou o dataset mais consistente e apropriado para algoritmos de regressão e aprendizado de máquina, reduzindo a influência de valores extremos e melhorando a estabilidade dos modelos.
