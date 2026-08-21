[README.md](https://github.com/user-attachments/files/31290294/README.md)
# gqs-algoritmo-01-py# Desafio de Lógica — Investigação de Palíndromos

![Python](https://img.shields.io/badge/Python-3.x-blue)
![GitHub](https://img.shields.io/badge/GitHub-Repositório-black)
![Markdown](https://img.shields.io/badge/Markdown-Documentação-green)

## Nível 1 — O Básico da Investigação

> 💡 **Dica visual:** os blocos marcados como `python`, `bash`, `console` e `regex` aparecem com cores automaticamente no GitHub, facilitando a leitura do código.


### O que o código faz?

Neste desafio, o programa analisa uma frase para verificar se ela é um **palíndromo**.

Um palíndromo é uma palavra ou frase que pode ser lida de frente para trás e de trás para frente e continua igual.

Por exemplo:

```text
ovo
```

Ao contrário, continua sendo:

```text
ovo
```

No programa, a frase passa por uma limpeza antes da comparação. O código remove alguns caracteres, transforma todas as letras em minúsculas, inverte o texto e compara o resultado.

Se o texto normal for igual ao texto invertido, o programa retorna `True`. Caso contrário, retorna `False`.

---

### Como executar?

Como este repositório está em **Python**, não é necessário compilar o arquivo antes da execução.

Primeiro, abro o terminal na pasta onde está o arquivo:

```bash
cd C:\Users\grafi\Downloads
```

Depois executo:

```bash
python DesafioLogica.py
```

O programa é executado e os resultados aparecem diretamente no terminal.

> Observação: o enunciado cita `javac` e `java`, que são comandos utilizados em projetos Java. Como este projeto utiliza Python, o comando correto para execução é `python DesafioLogica.py`.

---

### Exemplo de saída

Ao executar o programa, o terminal apresenta:

```console
Teste 1: False
Teste 2: True
```

Esses foram os resultados reais obtidos durante a execução.

---

## Nível 2 — Engenharia Reversa e Análise de Comportamento

### Desvendando os métodos

#### Qual é o papel do `main`?

No Python, o programa utiliza:

```python
if __name__ == "__main__":
```

Essa estrutura verifica se o arquivo está sendo executado diretamente.

Quando isso acontece, o programa cria as duas frases de teste:

```python
texto1 = "A sacada da casa de cadá"
texto2 = "Socorram-me, subi no ônibus em Marrocos"
```

Depois, cada frase é enviada para a função `analisar()` e o resultado é mostrado no terminal:

```python
print(f"Teste 1: {analisar(texto1)}")
print(f"Teste 2: {analisar(texto2)}")
```

Na prática, considero essa parte como o ponto de partida do programa, porque é ali que os testes são executados.

---

### Entendendo a função `analisar(entrada)`

A função começa assim:

```python
def analisar(entrada):
```

Ela recebe um texto chamado `entrada` e verifica se esse texto pode ser considerado um palíndromo.

#### 1. Verificação da entrada

```python
if entrada is None:
    return False
```

Essa parte verifica se existe algum conteúdo para analisar.

Se a entrada for `None`, ou seja, se não houver texto, a função retorna `False` e encerra a análise.

---

#### 2. Limpeza do texto

```python
limpa = re.sub(r'[^a-zA-Z0-9]', '', entrada).lower()
```

Essa foi uma das linhas que mais precisei observar para entender o comportamento dos testes.

A função `re.sub()` faz substituições no texto usando uma expressão regular.

A expressão:

```regex
[^a-zA-Z0-9]
```

procura qualquer caractere que **não seja** uma letra de `a` até `z`, uma letra de `A` até `Z` ou um número de `0` até `9`.

Esses caracteres são substituídos por uma string vazia:

```python
''
```

Na prática, isso remove espaços, vírgulas, hífens e outros caracteres especiais.

Depois, o método:

```python
.lower()
```

transforma todas as letras em minúsculas.

Isso evita que uma letra maiúscula seja considerada diferente da mesma letra minúscula.

---

#### 3. Inversão do texto

```python
invertida = limpa[::-1]
```

Essa linha inverte o texto já limpo.

O `[::-1]` é um recurso de fatiamento do Python chamado *slicing*.

Por exemplo:

```text
casa
```

fica:

```text
asac
```

---

#### 4. Comparação

```python
return limpa == invertida
```

Aqui o programa compara o texto limpo com o texto invertido.

Se forem iguais, retorna:

```python
True
```

Se forem diferentes, retorna:

```python
False
```

---

### O Mistério dos Testes

Quando executei o programa, obtive:

```console
Teste 1: False
Teste 2: True
```

#### Teste 1

A primeira frase é:

```text
A sacada da casa de cadá
```

O resultado foi:

```python
False
```

O motivo está na expressão regular utilizada:

```python
[^a-zA-Z0-9]
```

Ela aceita apenas letras sem acento e números.

Por isso, o caractere `á` não é considerado uma letra válida pela expressão e acaba sendo removido durante a limpeza.

Com essa remoção, o conteúdo analisado é alterado e a comparação com o texto invertido não resulta em igualdade.

Por isso, o Teste 1 retorna `False`.

---

#### Teste 2

A segunda frase é:

```text
Socorram-me, subi no ônibus em Marrocos
```

O resultado foi:

```python
True
```

Durante a limpeza, os espaços, o hífen, a vírgula e os caracteres que não correspondem ao padrão definido são removidos.

Depois dessa limpeza, o texto resultante forma uma sequência que continua igual quando invertida.

Por esse motivo, a comparação:

```python
limpa == invertida
```

resulta em `True`.

---

## Nível 3 — Toque Profissional

### Resumo do funcionamento

| Etapa | O que acontece |
|---|---|
| 1 | O programa recebe uma frase |
| 2 | Verifica se a entrada é válida |
| 3 | Remove caracteres que não fazem parte do padrão |
| 4 | Transforma as letras em minúsculas |
| 5 | Inverte o texto |
| 6 | Compara o texto normal com o invertido |
| 7 | Retorna `True` ou `False` |

### Resultados dos testes

| Teste | Frase | Resultado |
|---|---|---|
| Teste 1 | `A sacada da casa de cadá` | `False` |
| Teste 2 | `Socorram-me, subi no ônibus em Marrocos` | `True` |

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

## Sobre a Autora

**Michele Carvalho**

Sou estudante de Ciência da Computação e realizei este desafio com o objetivo de entender melhor a lógica do código, observar seu comportamento e documentar o que acontece durante a execução.

Este repositório foi criado a partir de um **fork do projeto original**, e a documentação foi desenvolvida como parte da atividade proposta.

Durante a análise, procurei explicar o código de forma simples e direta, registrando também o comportamento real dos testes e o motivo dos resultados encontrados.
