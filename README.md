# Desafio de Lógica — Investigação de Palíndromos

![Python](https://img.shields.io/badge/Python-3.x-blue)
![GitHub](https://img.shields.io/badge/GitHub-Repositório-black)
![Markdown](https://img.shields.io/badge/Markdown-Documentação-green)

Este projeto faz parte de uma atividade de investigação e análise de código. O objetivo foi entender como o programa funciona, observar o comportamento dos testes e documentar os resultados encontrados.

---

# Nível 1 — O Básico da Investigação

## O que o código faz?

O programa tem como objetivo verificar se uma palavra ou frase pode ser considerada um **palíndromo**.

Um palíndromo é uma palavra ou frase que pode ser lida de frente para trás e de trás para frente da mesma maneira.

Um exemplo simples é:

```text
ovo
```

Ao inverter a palavra, o resultado continua sendo:

```text
ovo
```

No programa analisado, a frase passa por algumas etapas antes da comparação.

Primeiro, alguns caracteres são removidos. Depois, todas as letras são transformadas em minúsculas. Em seguida, o texto é invertido.

No final, o programa compara o texto limpo com o texto invertido.

Se forem iguais, retorna:

```python
True
```

Caso sejam diferentes, retorna:

```python
False
```

---

## Como executar?

Como este projeto utiliza **Python**, não é necessário compilar o arquivo antes de executar.

Primeiro, abro o terminal na pasta onde o arquivo está salvo.

No meu caso:

```bash
cd C:\Users\grafi\Downloads
```

Depois executo o programa com:

```bash
python DesafioLogica.py
```

Após executar o comando, o Python roda o arquivo e apresenta os resultados diretamente no terminal.

> **Observação:** o enunciado da atividade cita os comandos `javac` e `java`, que são utilizados na linguagem Java. Como este repositório utiliza Python, o comando utilizado para executar o programa é `python DesafioLogica.py`.

---

## Exemplo de saída

Ao executar o programa, o console apresenta:

```console
Teste 1: False
Teste 2: True
```

Esses foram os resultados reais encontrados durante a execução do programa.

---

# Nível 2 — Engenharia Reversa e Análise de Comportamento

## Desvendando os métodos

### Qual é o papel do `main`?

No Python, o programa utiliza a seguinte estrutura:

```python
if __name__ == "__main__":
```

Essa estrutura verifica se o arquivo está sendo executado diretamente.

Quando isso acontece, o programa cria duas frases para serem utilizadas nos testes:

```python
texto1 = "A sacada da casa de cadá"
texto2 = "Socorram-me, subi no ônibus em Marrocos"
```

Depois, cada uma dessas frases é enviada para a função `analisar()`.

```python
print(f"Teste 1: {analisar(texto1)}")
print(f"Teste 2: {analisar(texto2)}")
```

Os resultados retornados pela função são mostrados no terminal.

De forma simples, considero essa parte como o ponto de partida do programa, pois é nela que os testes são executados.

---

## Entendendo a função `analisar(entrada)`

A função começa da seguinte forma:

```python
def analisar(entrada):
```

Ela recebe um texto chamado `entrada` e analisa se esse texto pode ser considerado um palíndromo.

### 1. Verificação da entrada

```python
if entrada is None:
    return False
```

Essa parte verifica se existe algum conteúdo para ser analisado.

Se a entrada for `None`, significa que não existe texto para analisar.

Nesse caso, a função retorna:

```python
False
```

e encerra a execução.

---

### 2. Limpeza do texto

Depois temos:

```python
limpa = re.sub(r'[^a-zA-Z0-9]', '', entrada).lower()
```

Essa foi uma das partes mais importantes para entender o comportamento do programa.

A função:

```python
re.sub()
```

faz substituições dentro de um texto utilizando uma expressão regular.

A expressão usada é:

```regex
[^a-zA-Z0-9]
```

Ela procura qualquer caractere que **não seja**:

* uma letra de `a` até `z`;
* uma letra de `A` até `Z`;
* um número de `0` até `9`.

Os caracteres encontrados são substituídos por:

```python
''
```

Ou seja, são removidos.

Na prática, isso pode remover espaços, vírgulas, hífens, acentos e outros caracteres que não estejam dentro do padrão definido.

Depois é utilizado:

```python
.lower()
```

Esse método transforma todas as letras em minúsculas.

Por exemplo:

```text
OVO
```

passa a ser:

```text
ovo
```

Isso evita que letras maiúsculas e minúsculas sejam consideradas diferentes durante a comparação.

---

### 3. Inversão do texto

Depois aparece:

```python
invertida = limpa[::-1]
```

Essa linha inverte o texto que já foi limpo.

O:

```python
[::-1]
```

é um recurso do Python chamado **slicing**, ou fatiamento.

Por exemplo:

```text
casa
```

quando invertida fica:

```text
asac
```

---

### 4. Comparação

Por último, temos:

```python
return limpa == invertida
```

Aqui o programa compara o texto limpo com o texto invertido.

Se os dois forem iguais, o resultado será:

```python
True
```

Se forem diferentes:

```python
False
```

---

# O Mistério dos Testes

Ao executar o programa, obtive:

```console
Teste 1: False
Teste 2: True
```

## Teste 1

A primeira frase analisada é:

```text
A sacada da casa de cadá
```

O programa retorna:

```python
False
```

O motivo está relacionado à expressão regular:

```regex
[^a-zA-Z0-9]
```

Essa expressão aceita apenas letras sem acento e números.

Por isso, o caractere:

```text
á
```

não é considerado válido pelo padrão e acaba sendo removido durante a limpeza.

Com essa remoção, o texto utilizado na comparação é alterado.

Quando o programa compara o texto limpo com o texto invertido, eles não são iguais.

Por isso o resultado do Teste 1 é:

```python
False
```

---

## Teste 2

A segunda frase é:

```text
Socorram-me, subi no ônibus em Marrocos
```

O resultado apresentado foi:

```python
True
```

Durante a limpeza, espaços, hífen, vírgula e caracteres que não fazem parte do padrão utilizado são removidos.

Depois dessa limpeza, o texto resultante forma uma sequência que continua igual quando é invertida.

Por isso, a comparação:

```python
limpa == invertida
```

resulta em:

```python
True
```

---

# Nível 3 — Toque Profissional

## Tecnologias utilizadas

| Tecnologia | Utilização                                |
| ---------- | ----------------------------------------- |
| Python     | Desenvolvimento e execução do programa    |
| Regex      | Limpeza e tratamento do texto             |
| Markdown   | Documentação do projeto                   |
| GitHub     | Versionamento e publicação do repositório |

---

## Fluxo do programa

1. O programa recebe uma frase.
2. Verifica se existe uma entrada válida.
3. Remove caracteres que não fazem parte do padrão.
4. Transforma todas as letras em minúsculas.
5. Inverte o texto.
6. Compara o texto limpo com o texto invertido.
7. Retorna `True` ou `False`.

---

## Resultados dos testes

| Teste   | Frase analisada                           | Resultado |
| ------- | ----------------------------------------- | --------- |
| Teste 1 | `A sacada da casa de cadá`                | `False`   |
| Teste 2 | `Socorram-me, subi no ônibus em Marrocos` | `True`    |

---

## Código analisado

```python
import re

def analisar(entrada):
    if entrada is None:
        return False

    limpa = re.sub(r'[^a-zA-Z0-9]', '', entrada).lower()

    invertida = limpa[::-1]

    return limpa == invertida


if __name__ == "__main__":
    texto1 = "A sacada da casa de cadá"
    texto2 = "Socorram-me, subi no ônibus em Marrocos"

    print(f"Teste 1: {analisar(texto1)}")
    print(f"Teste 2: {analisar(texto2)}")
```

---

# Sobre a Autora

**Michele Carvalho**

Sou estudante de Ciência da Computação e realizei este desafio com o objetivo de compreender melhor a lógica de programação, analisar o comportamento do código e praticar documentação utilizando Markdown.

Este repositório foi criado a partir de um **fork do projeto original**.

Durante a atividade, procurei entender cada parte do código, executar os testes e investigar por que cada resultado aconteceu.

A documentação foi organizada utilizando títulos, listas, tabelas, badges e blocos de código para facilitar a leitura e deixar o projeto mais organizado.
