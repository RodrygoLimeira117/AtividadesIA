# 🔬 Pré-processamento e Limpeza de Dados: Dataset Iris Corrompido

## 📋 Objetivo da Atividade

O objetivo deste projeto foi aplicar técnicas essenciais de **pré-processamento de dados** em um dataset simulado do Iris que contém falhas (valores nulos - `NaN`) e valores atípicos (*outliers*). A missão foi limpar e preparar o conjunto de dados para garantir sua qualidade e adequação para futuras análises e modelagem de Machine Learning.

O notebook `atividade 1.py.ipynb` detalha a execução dos seguintes passos:
1.  **Carregamento e Análise Inicial** dos dados.
2.  **Tratamento de Dados Faltantes** (Imputação).
3.  **Identificação e Tratamento de Outliers** (Técnica de *Capping*).
4.  **Verificação Final** das estatísticas e distribuição dos dados.

---

## 🛠️ Metodologia e Técnicas Aplicadas

### 1. Tratamento de Dados Faltantes (Imputação por Mediana)

A inspeção inicial revelou que as quatro colunas de medição (`SepalLengthCm`, `SepalWidthCm`, `PetalLengthCm`, `PetalWidthCm`) continham valores nulos.

| Coluna | Contagem de Nulos | Estratégia de Imputação |
| :--- | :---: | :--- |
| `SepalLengthCm` | 15 | Mediana |
| `SepalWidthCm` | 14 | Mediana |
| `PetalLengthCm` | 15 | Mediana |
| `PetalWidthCm` | 15 | Mediana |

A **mediana** foi escolhida como técnica de imputação para mitigar a influência de possíveis *outliers* na distribuição, garantindo que os valores imputados representem o centro da distribuição original de forma robusta.

#### Medidas de Mediana Calculadas:

* Mediana de `SepalLengthCm`: **5.8**
* Mediana de `SepalWidthCm`: **3.0**
* Mediana de `PetalLengthCm`: **4.2**
* Mediana de `PetalWidthCm`: **1.3**

---

### 2. Tratamento de Outliers (*Capping* via IQR)

Os *boxplots* gerados antes do tratamento  indicaram que a coluna **`SepalWidthCm`** apresentava os *outliers* mais significativos (pontos isolados acima do bigode superior).

Para tratar esses valores atípicos, foi utilizado o método **Intervalo Interquartil (IQR)** e a técnica de **Capping** (limitação).

#### Cálculo do Limite Superior para `SepalWidthCm`:

O limite foi calculado usando a fórmula: $Q3 + 1.5 \cdot IQR$.

| Métrica | Valor |
| :--- | :--- |
| **Q1** (25º Percentil) | 2.80 |
| **Q3** (75º Percentil) | 3.30 |
| **IQR** ($Q3 - Q1$) | 0.50 |
| **Limite Superior** | **4.05** |

#### Aplicação do Capping:

Todos os valores na coluna `SepalWidthCm` que eram **maiores** que o `Limite Superior` de **4.05** foram substituídos por **4.05**. Esta técnica (*capping*) evita a remoção de registros e a distorção da distribuição, comprimindo os *outliers* para a fronteira aceitável.

---

## 📈 Resultados Finais

Após a imputação de valores faltantes e o tratamento dos *outliers* por *capping*, o dataset foi submetido a uma inspeção final.

### Estatísticas Descritivas do Dataset Limpo

O método `.describe()` confirma o sucesso do tratamento, mostrando que a contagem de registros (`count`) é 150 para todas as colunas, e o valor máximo de `SepalWidthCm` foi limitado.

| Estatística | SepalLengthCm | SepalWidthCm | PetalLengthCm | PetalWidthCm |
| :--- | :---: | :---: | :---: | :---: |
| **count** | 150.000000 | 150.000000 | 150.000000 | 150.000000 |
| **mean** | 5.839333 | **3.077333** | 3.736000 | 1.200667 |
| **std** | 0.777787 | **0.417792** | 1.656603 | 0.723294 |
| **min** | 4.300000 | 2.200000 | 1.000000 | 0.100000 |
| **25%** | 5.200000 | 2.800000 | 1.600000 | 0.400000 |
| **50%** | 5.800000 | 3.000000 | 4.200000 | 1.300000 |
| **75%** | 6.375000 | 3.300000 | 4.900000 | 1.800000 |
| **max** | 7.900000 | **4.050000** | 6.900000 | 2.500000 |

*Observação: O valor **máximo** para `SepalWidthCm` agora é **4.05**, que é exatamente o limite superior calculado pelo IQR, confirmando a aplicação do *capping*.

### Boxplot Final (SepalWidthCm)

O novo boxplot de `SepalWidthCm`  demonstra que os pontos atípicos foram limitados, resultando em uma distribuição visualmente mais limpa e pronta para a análise.

---

## 👨‍💻 Autor(es)

José Rodrigo Araujo Limeira
