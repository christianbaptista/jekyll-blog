---
layout: post
title: A Definição Formal de um Neurônio Artificial
date: 2024-11-26
categories: ["matrix", "AI", "neural", "artificial neural"]
---


![Dummy Image 1](https://picsum.photos/1366/768)

Contexto:


O conceito de neurônio artificial é aplicado em uma tarefa de classificação binária, onde existem duas classes:

-    **Classe positiva**: representada por +1
-    **Classe negativa**: representada por -1


# Definição Formal de um Neurônio Artificial


## 1. Entrada e Função de Decisão

### **Entradas**
A entrada é um vetor \( x \), contendo os valores das entradas do neurônio:

\[x =
\begin{array}
x_1 \\
x_2 \\
\vdots \\
x_m
\end{array}
\]

### **Pesos**
O vetor de pesos \( w \), associado às entradas, é:
\[
w =
\begin{bmatrix}
w_1 \\
w_2 \\
\vdots \\
w_m
\end{bmatrix}
\]

### **Combinação Linear (Net Input)**
A combinação linear das entradas e pesos (\( z \), também chamado de **net input** ou **entrada líquida**) é:
\[
z = w_1x_1 + w_2x_2 + \dots + w_mx_m = w^T x
\]

---

## 2. Função de Ativação

A **função de ativação** \( \phi(z) \) determina a saída do neurônio com base no valor de \( z \):
\[
\phi(z) =
\begin{cases}
1 & \text{se } z \geq \theta \\
-1 & \text{se } z < \theta
\end{cases}
\]
Onde \( \theta \) é o **limiar (threshold)**.

---

## 3. Simplificação: Uso de Bias

### **Movendo o Limiar**
Para simplificar os cálculos, o limiar \( \theta \) é movido para o lado esquerdo da equação:
\[
z - \theta \geq 0 \implies z = w_0x_0 + w_1x_1 + \dots + w_mx_m
\]

### **Introduzindo o Bias**
Introduz-se um termo chamado **bias** (\( w_0 = -\theta \)) e define-se \( x_0 = 1 \). Assim, a fórmula é reescrita como:
\[
z = w_0x_0 + w_1x_1 + \dots + w_mx_m = w^T x
\]

---

## 4. Função de Ativação (Simplificada)
Com essa modificação, a função de ativação se torna:
\[
\phi(z) =
\begin{cases}
1 & \text{se } z \geq 0 \\
-1 & \text{se } z < 0
\end{cases}
\]

---

## **Nota sobre o Bias**
Na literatura de aprendizado de máquina, o termo \( w_0 \) (bias) é usado para ajustar o **limiar de decisão** sem depender diretamente das entradas. Isso flexibiliza o modelo ao permitir ajustes no ponto de corte entre as classes.

## **Problema:**
Queremos criar um neurônio que decide se um aluno será aprovado ou não com base em **duas notas**:
- \(x_1\): Nota da prova (**peso maior**, pois é mais importante).
- \(x_2\): Nota de participação.

O neurônio calculará uma **pontuação final** (\(z\)) e determinará:
- **Aprovado (\(+1\))**: Se \(z \geq 0\).
- **Reprovado (\(-1\))**: Se \(z < 0\).

---

## **Configuração do Neurônio**
1. **Pesos (\(w_1, w_2\)) e Bias (\(w_0\)):**
   - \(w_1 = 0.7\) (peso para a prova).
   - \(w_2 = 0.3\) (peso para a participação).
   - \(w_0 = -0.5\) (bias ajusta o limiar para \(z = 0\)).

2. **Entradas (\(x_1, x_2\)):**
   - \(x_1 = 0.8\) (nota da prova, variando de 0 a 1).
   - \(x_2 = 0.6\) (nota de participação, variando de 0 a 1).

3. **Fórmula para o \(z\):**
   \[
   z = w_0 + w_1 x_1 + w_2 x_2
   \]

---

## **Cálculo do \(z\):**
Substituímos os valores na fórmula:
\[
z = (-0.5) + (0.7 \cdot 0.8) + (0.3 \cdot 0.6)
\]

### Passo a passo:
1. \(0.7 \cdot 0.8 = 0.56\)
2. \(0.3 \cdot 0.6 = 0.18\)
3. Soma total: \(-0.5 + 0.56 + 0.18 = 0.24\)

---

## **Classificação (\(\phi(z)\)):**
Usamos a função de ativação:
\[
\phi(z) =
\begin{cases}
1 & \text{se } z \geq 0 \\
-1 & \text{se } z < 0
\end{cases}
\]

Como \(z = 0.24 \geq 0\), a saída é:
\[
\phi(z) = +1 \, (\text{Aprovado})
\]

---

## **Resumo do Exemplo**
- **Entradas:**
  - Nota da prova (\(x_1\)): **0.8**
  - Nota de participação (\(x_2\)): **0.6**

- **Cálculo:**
  - $$ (z = 0.24) $$

- **Classificação:**
  - Saída: **+1 (Aprovado)**

O bias (\(w_0 = -0.5\)) ajustou o limiar de decisão para \(z = 0\), tornando o cálculo mais flexível.

---

## **Conclusão**
Este exemplo mostra como um neurônio artificial funciona:
1. Combina pesos e entradas em uma fórmula linear (\(z\)).
2. Usa a **função de ativação** para decidir a saída (\(+1\) ou \(-1\)).
3. O bias permite ajustar o limiar de decisão sem alterar os pesos das entradas.
