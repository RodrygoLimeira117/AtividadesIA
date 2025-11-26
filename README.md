# 🚀 Projeto: Implementação do Perceptron Simples

## 🎓 Visão Geral do Projeto

Este projeto implementa o algoritmo de treinamento do **Perceptron Simples** em Python utilizando a biblioteca NumPy. O Perceptron, o bloco de construção mais fundamental das redes neurais, é um modelo de classificação binária e linear supervisionada, desenvolvido por Frank Rosenblatt em 1957.

O objetivo é demonstrar o aprendizado dos pesos para um conjunto de dados linearmente separável, simulando o exercício prático da aula de [Nome da Disciplina].

---

## 🧠 Fundamentos Teóricos do Perceptron

O Perceptron opera através de uma função de ativação de passo (step function) após calcular o *net input*.

### 1. Net Input (Entrada Líquida)

O net input ($net$) é a soma ponderada dos atributos de entrada ($\mathbf{x}$) pelos seus respectivos pesos ($\mathbf{w}$):

$$\text{net} = w_0 + \sum_{j=1}^{m} w_j x_j = \mathbf{w}^T \mathbf{x}$$

### 2. Função de Ativação (Output)

A saída ($\hat{y}$) do Perceptron é determinada pela função sinal (sign function):

$$\hat{y} = \begin{cases} +1 & \text{se } \text{net} \ge 0 \\ -1 & \text{se } \text{net} < 0 \end{cases}$$

### 3. Regra de Aprendizagem (Atualização de Pesos)

O Perceptron é treinado usando a regra delta (ou regra Perceptron), que só atualiza os pesos em caso de erro ($\hat{y} \neq y$).

O ajuste do peso ($\Delta w_j$) e a atualização do novo peso ($w_{j, novo}$) são dados por:

$$\Delta w_j = \alpha \cdot (y - \hat{y}) \cdot x_j$$
$$w_{j, novo} = w_{j, antigo} + \Delta w_j$$

Onde $\alpha$ é a **taxa de aprendizagem**.

---

## 🛠️ Detalhes da Implementação

### Estrutura do Arquivo

| Arquivo | Descrição |
| :--- | :--- |
| `perceptron_algorithm.py` | Contém a função principal `perceptron_train()` e o script de teste. |
| `README.md` | Este documento. |

### Dados de Treinamento

O dataset utilizado inclui o termo de **bias ($X_0=1$)** adicionado ao vetor de atributos, resultando em $X = [X_0, X_1, X_2]$.

| Exemplo | $X_1$ | $X_2$ | Classe $Y$ | Vetor de Entrada ($X$) |
| :-----: | :---: | :---: | :--------: | :-------------------: |
| 0 | 1 | 1 | 1 | `[1, 1, 1]` |
| 1 | 0 | 1 | 1 | `[1, 0, 1]` |
| 2 | 0 | 0 | -1 | `[1, 0, 0]` |
| 3 | 1 | 0 | -1 | `[1, 1, 0]` |

### Parâmetros

* **Pesos Iniciais ($\mathbf{w}$):** `[0.0, 0.0, 0.0]`
* **Taxa de Aprendizagem ($\alpha$):** `0.5`

---

## 📊 Resultados e Convergência

O treinamento demonstrou **convergência** em 4 épocas, classificando corretamente todos os exemplos.

### Logs Detalhados de Atualização de Pesos

A tabela mostra apenas os passos onde ocorreu erro de classificação e os pesos foram ajustados:

| Época | Exemplo (i) | $x$ (com bias) | $y_{verdadeiro}$ | $y_{predito}$ | $w_{antigo}$ | $\Delta w$ | $w_{novo}$ |
| :---: | :---------: | :------------: | :--------------: | :-----------: | :----------: | :--------: | :--------: |
| **1** | 2 | [1, 0, 0] | -1 | 1 | [0.0, 0.0, 0.0] | [-1, 0, 0] | **[-1.0, 0.0, 0.0]** |
| **2** | 0 | [1, 1, 1] | 1 | -1 | [-1.0, 0.0, 0.0] | [1, 1, 1] | [0.0, 1.0, 1.0] |
| **2** | 2 | [1, 0, 0] | -1 | 1 | [0.0, 1.0, 1.0] | [-1, 0, 0] | [-1.0, 1.0, 1.0] |
| **2** | 3 | [1, 1, 0] | -1 | 1 | [-1.0, 1.0, 1.0] | [-1, -1, 0] | **[-2.0, 0.0, 1.0]** |
| **3** | 0 | [1, 1, 1] | 1 | -1 | [-2.0, 0.0, 1.0] | [1, 1, 1] | [-1.0, 1.0, 2.0] |
| **3** | 3 | [1, 1, 0] | -1 | 1 | [-1.0, 1.0, 2.0] | [-1, -1, 0] | **[-2.0, 0.0, 2.0]** |
| **4** | **Convergência** | N/A | N/A | N/A | N/A | N/A | **[-2.0, 0.0, 2.0]** |

### Pesos Finais

$$\mathbf{w}_{final} = [-2.0, 0.0, 2.0]$$

### Equação do Hiperplano (Fronteira de Decisão)

O hiperplano de separação linear é definido pela equação $\mathbf{w}^T \mathbf{x} = 0$:

$$-2.0 \cdot 1 + 0.0 \cdot x_1 + 2.0 \cdot x_2 = 0$$
$$2x_2 = 2$$
$$\mathbf{x_2 = 1}$$

A fronteira de decisão é uma linha horizontal em $x_2=1$.

---

## 👨‍💻 Autores

* [Seu Nome / Matrícula]
* [Nome da Dupla / Matrícula (se aplicável)]
