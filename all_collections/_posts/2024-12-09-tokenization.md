---
layout: post
title: Tokenizar por que é importante?
date: 2024-01-22
categories: ["python", "NLT", "ML", "AI", "NLTK", "spaCy"]
---


![Dummy Image 1](https://picsum.photos/1366/768)

A tokenização é uma etapa fundamental no processamento de linguagem natural (PLN) e em outras áreas que envolvem manipulação de texto. Trata-se do processo de dividir um texto em unidades menores, chamadas tokens, que podem ser palavras, símbolos ou mesmo partes de palavras.

## Intro

A tokenização é essencial para preparar textos para análises e modelagens. Algumas das principais razões para a sua importância incluem:

- Estruturação de Dados: Textos são convertidos em uma forma que é compreensível para métodos computacionais.

- Análise Semântica: Permite identificar palavras-chave, relações entre termos e significados no contexto do texto.

- Treinamento de Modelos: É uma etapa inicial para criar entradas para algoritmos de aprendizado de máquina ou deep learning.

## Alguns casos de uso

1. Análise de Sentimento: Dividir textos de avaliações para determinar opiniões positivas ou negativas.

2. Sistemas de Busca: Melhorar a relevância dos resultados, identificando termos significativos em consultas.

3. Tradução Automática: Separar as palavras e compreender sua estrutura antes de traduzir.

## Sem enrolação vamos para prática.

A seguir, apresentamos dois exemplos utilizando bibliotecas populares de Python: NLTK e spaCy.

1. Tokenização com NLTK

O NLTK (Natural Language Toolkit) é uma das bibliotecas mais populares para PLN em Python.

```python
import nltk
from nltk.tokenize import word_tokenize

# Certifique-se de baixar os recursos necessários antes
nltk.download('punkt')

texto = "A tokenização é essencial para PLN."

tokens = word_tokenize(texto)
print("Tokens:", tokens)
```

Output:

```python
Tokens: ['A', 'tokenização', 'é', 'essencial', 'para', 'PLN', '.']
```

2. Tokenização com spaCy

O spaCy é uma biblioteca voltada para processamento de linguagem natural com foco em desempenho e eficiência.

```python
import spacy

# Carregue o modelo de linguagem
nlp = spacy.load("pt_core_news_sm")

texto = "A tokenização é essencial para PLN."

doc = nlp(texto)
tokens = [token.text for token in doc]
print("Tokens:", tokens)
```

Output:

```python
Tokens: ['A', 'tokenização', 'é', 'essencial', 'para', 'PLN', '.']
```
Pode-se destacar que a tokenização, especialmente para modelos que utilizam subpalavras, deve considerar o contexto em que as palavras aparecem. Expressões idiomáticas frequentemente têm significado não-composicional, e fragmentar essas frases em tokens menores (por exemplo, "under", "the", "weather") pode prejudicar a capacidade do modelo de capturar o significado correto.


- Tokenização e Contexto Semântico: Explique que a simples divisão em tokens pode não ser suficiente, especialmente para expressões idiomáticas.
- Impacto nos Modelos de Linguagem: Relate como modelos como BERT usam embeddings para diferenciar usos literais e idiomáticos, mostrando a importância de estratégias de tokenização mais avançadas.
- Exemplo Prático: Use uma ferramenta como o Hugging Face Transformers para demonstrar como a representação muda em contextos diferentes.

**Código Exemplo**

Você pode incluir um exemplo no seu artigo para ilustrar a análise mencionada:
```python
from transformers import AutoTokenizer, AutoModel
import torch

# Carregar modelo pré-treinado
tokenizer = AutoTokenizer.from_pretrained("bert-base-uncased")
model = AutoModel.from_pretrained("bert-base-uncased")

# Frases para análise
idiomatic_sentence = "I’m feeling under the weather." # Estou me sentindo debaixo do tempo, mas na verdade representa: não estou me sentindo bem
literal_sentence = "I’m feeling unwell today." # que é o que essa sentença significa...

# Tokenização
inputs_idiom = tokenizer(idiomatic_sentence, return_tensors="pt")
inputs_literal = tokenizer(literal_sentence, return_tensors="pt")

# Obter embeddings
outputs_idiom = model(**inputs_idiom)
outputs_literal = model(**inputs_literal)

# Extração do embedding da camada final
embedding_idiom = outputs_idiom.last_hidden_state.mean(dim=1)
embedding_literal = outputs_literal.last_hidden_state.mean(dim=1)

# Similaridade de cosseno
cosine_similarity = torch.nn.functional.cosine_similarity(embedding_idiom, embedding_literal)
print("Similaridade de cosseno entre contexto idiomático e literal:", cosine_similarity.item())
```
# Mas como isso funciona na realidade dentro de uma LLM ou algo semelhante?

Existem algumas formas hoje iremos analizar **Similaridade de Cosseno**.
Utilizando a similaridade de cosseno para medir a proximidade entre embeddings de palavras ou frases em diferentes contextos (idiomático e literal). Essa equação é amplamente utilizada em processamento de linguagem natural (PLN) para comparar vetores de alta dimensão.

## Equação de Similaridade de Cosseno

A similaridade de cosseno é calculada da seguinte forma:

$$
\text{Sim}(A, B) = \frac{A \cdot B}{\|A\| \|B\|}
$$

Onde:

- AA e BB são os vetores de embedding.
- A⋅BA⋅B é o produto escalar entre os dois vetores.
- ∥A∥∥A∥ e ∥B∥∥B∥ são as normas dos vetores.


**Embedding de Frases e Palavras**: Cada frase ou palavra é transformada em um vetor de alta dimensão por meio do modelo BERT. Esses vetores capturam características semânticas e contextuais.
**Comparação de Contextos**:
  1. A similaridade de cosseno é usada para avaliar a proximidade entre o embedding de uma palavra em um contexto idiomático e o embedding da mesma palavra em um contexto literal.
  2. Valores mais baixos para contextos idiomáticos indicam uma maior diferença semântica.

O valor da similaridade varia entre -1 e 1:


- 1 indica que os vetores estão perfeitamente alinhados (máxima similaridade).
- 0 indica que os vetores são ortogonais (sem similaridade).
- -1 indica que os vetores estão opostos.

Suponha que os vetores embedding AA (idiomático) e BB (literal) sejam:

$$
\|A\| = \sqrt{\sum_{i=1}^{n} A_i^2}, \quad \|B\| = \sqrt{\sum_{i=1}^{n} B_i^2}
$$

1. Produto Escalar:

$$
A \cdot B = (A_1 \cdot B_1) + (A_2 \cdot B_2) + \dots + (A_n \cdot B_n)
$$

2. Norma dos Vetores:

$$
\|A\| = \sqrt{A_1^2 + A_2^2 + \dots + A_n^2}, \quad \|B\| = \sqrt{B_1^2 + B_2^2 + \dots + B_n^2}
$$


3. Similaridade de Cosseno:

$$
\text{Sim}(A, B) = \frac{(A_1 \cdot B_1) + (A_2 \cdot B_2) + \dots + (A_n \cdot B_n)}{\sqrt{A_1^2 + A_2^2 + \dots + A_n^2} \cdot \sqrt{B_1^2 + B_2^2 + \dots + B_n^2}}
$$

Esse valor indica alta similaridade entre os vetores, o que poderia representar, por exemplo, uma palavra com significado semelhante nos dois contextos.

# Conclusão
A tokenização é um passo crucial no processamento de texto, servindo como base para aplicações em inteligência artificial, análises e busca de informações. Bibliotecas como NLTK e spaCy tornam esse processo simples e eficiente, permitindo que desenvolvedores e pesquisadores explorem as nuances da linguagem com facilidade. Em projetos de LLMs e DL, a tokenização não apenas facilita a interpretação semântica, mas também é essencial para o desempenho e a escalabilidade dos modelos.
