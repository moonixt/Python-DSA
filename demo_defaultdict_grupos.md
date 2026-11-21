---
title: demo_defaultdict_grupos
date: 2026-11-20
tags:
  - python
  - dicionario
  - defaultdict
  - tupla
aliases:
  - defaultdict
  - breakdown demo_defaultdict_grupos
related: "[[demo_counter]]"
---

# demo_defaultdict_grupos

**1h 14min. 13 perguntas.** 20 nov 2026, 16:04–17:16. O intervalo vai do pedido de breakdown até a pergunta sobre a chamada. Pedidos de skill e da própria nota não entram na conta.

## Como as perguntas andaram

Nenhuma pergunta voltou para `def`, `->` ou `return`. O caminho novo foi o dado: o que é uma tupla, se o par é categoria e produto, se dá para inserir. O mapa das três funções está em [[Review]].

| Trabalho | Quantas | Onde apareceu |
|---|---|---|
| Destrava | 4 | `list` no parâmetro cria a lista; `list[tuple]` é uma lista que também é tupla; pacote fixo não se lê; a ordem do `for` |
| Confere | 6 | tupla como categoria e produto; lista no lugar da tupla; não dá para inserir; o exemplo das palavras na documentação |
| Leva | 3 | o pedido de breakdown da função inteira; a chamada com os pares; a leitura do `defaultdict` fora deste arquivo |

A checagem da documentação chegou certa: a chave é o primeiro caractere e a palavra inteira entra na lista. A dúvida do `while` desta função ainda não existia. Ela aparece na próxima.

Nota de estudo da função em `00_fase0_python_essentials.py`.

Nota de estudo da função em `00_fase0_python_essentials.py`. A casca é a mesma de [[demo_counter]]: `def`, nome, parâmetro com tipo, `->` com o tipo da saída, e o `return` no fim. Liga com [[Listas e dicionarios]].

```python
from collections import defaultdict

def demo_defaultdict_grupos(pares: list[tuple[str, str]]) -> dict[str, list[str]]:
    """Agrupa valores por chave sem testar 'if chave not in d'."""
    grupos: dict[str, list[str]] = defaultdict(list)
    for chave, valor in pares:
        grupos[chave].append(valor)
    return dict(grupos)
```

Chamada:

```python
demo_defaultdict_grupos([
    ("fruta", "uva"),
    ("fruta", "maçã"),
    ("cor", "azul"),
])
# {"fruta": ["uva", "maçã"], "cor": ["azul"]}
```

O corpo só roda nessa chamada. A função já definida no arquivo não executa o `for` sozinha.

## Ordem da função

A ordem, de cima para baixo e da esquerda para a direita, é: `def`, nome, parâmetro, tipo do parâmetro, tipo do retorno, `grupos`, tipo de `grupos`, `defaultdict(list)`, `for`, `chave` e `valor`, `pares`, `grupos[chave]`, `append`, `return`, `dict(grupos)`.

| Pedaço                    | O que é                                                                    |
| ------------------------- | -------------------------------------------------------------------------- |
| `def`                     | palavra que abre a definição da função                                     |
| `demo_defaultdict_grupos` | nome da função                                                             |
| `pares`                   | nome do parâmetro, a lista que entra                                       |
| `: list[tuple[str, str]]` | tipo dessa lista: cada item é um par de duas strings                       |
| `-> dict[str, list[str]]` | tipo da saída: chave string, valor lista de strings                        |
| `grupos`                  | variável que a função cria para guardar os grupos                          |
| `: dict[str, list[str]]`  | tipo dessa variável, o mesmo formato da saída                              |
| `= defaultdict(list)`     | cria o dicionário que abre uma lista vazia quando a chave ainda não existe |
| `for`                     | abre a repetição sobre a lista                                             |
| `chave, valor`            | os dois textos de cada par                                                 |
| `in pares`                | a lista de onde cada par sai                                               |
| `grupos[chave]`           | a lista guardada naquela chave                                             |
| `.append(valor)`          | acrescenta o texto no fim dessa lista                                      |
| `return`                  | devolve o valor para quem chamou                                           |
| `dict(grupos)`            | copia os grupos para um dicionário comum                                   |

## Ferramentas

```python
from collections import defaultdict
```

| Ferramenta | De onde vem | Papel nesta função | Documentação |
|---|---|---|---|
| `defaultdict` | `collections` | agrupa: chave nova ganha uma lista vazia, e o `append` coloca o item nessa lista | [defaultdict](https://docs.python.org/3/library/collections.html#collections.defaultdict) |
| `dict` | embutido do Python | copia os grupos para um dicionário comum | [dict](https://docs.python.org/3/library/stdtypes.html#dict) |
| `list` | embutido do Python | dentro de `defaultdict(list)`, fabrica a lista vazia da chave nova | [list](https://docs.python.org/3/library/stdtypes.html#list) |

`pares` é o nome. `list` na anotação `: list[tuple[str, str]]` é o tipo, e essa anotação não cria a lista. Quem chama cria a lista e entrega em `pares`.

O mesmo `defaultdict` agrupa palavras pela primeira letra:

```python
words = ["apple", "ant", "banana", "bat", "carrot", "cat"]
grouped = defaultdict(list)
for word in words:
    grouped[word[0]].append(word)
```

| Volta | `word` | `word[0]` | `grouped` no fim da volta |
|---|---|---|---|
| 1 | `"apple"` | `"a"` | `{"a": ["apple"]}` |
| 2 | `"ant"` | `"a"` | `{"a": ["apple", "ant"]}` |
| 3 | `"banana"` | `"b"` | `{"a": ["apple", "ant"], "b": ["banana"]}` |
| 4 | `"bat"` | `"b"` | `{"a": ["apple", "ant"], "b": ["banana", "bat"]}` |
| 5 | `"carrot"` | `"c"` | a lista de `"c"` nasce com `["carrot"]` |
| 6 | `"cat"` | `"c"` | `{"a": ["apple", "ant"], "b": ["banana", "bat"], "c": ["carrot", "cat"]}` |

Nesta função, a chave chega pronta no primeiro lugar da tupla. No exemplo das palavras, a chave é tirada da própria string, em `word[0]`. O `append` faz o mesmo serviço nos dois: põe o item inteiro na lista daquela chave.

## Tupla

Uma tupla é um pacote ordenado de valores. Nesta função, cada pacote é categoria e produto.

```python
("fruta", "uva")
```

| Posição | Valor | No `for` |
|---|---|---|
| 1º | `"fruta"` | `chave`, a categoria |
| 2º | `"uva"` | `valor`, o produto |

`list[tuple[str, str]]` se lê de fora para dentro: uma lista, e cada item da lista é uma tupla de duas strings. O tipo de um par só, sem a lista, seria `tuple[str, str]`.

A tupla é acessível: `par[0]` e `par[1]`. Pacote fixo quer dizer que ela permanece com os itens com que foi criada. Não existe `append` nela. Quem recebe item novo é a lista do dicionário, em `grupos[chave].append(valor)`.

O `for chave, valor` também aceita uma lista de listas, porque só precisa de dois lugares em ordem. A anotação acompanharia a troca e ficaria `list[list[str]]`. A função escreve tupla porque cada par é um pacote fixo.

## Ordem de execução

A tabela seguinte é a ordem de execução. As linhas continuam na ordem da leitura.

| Ordem na linha | Pedaço | Quando roda |
|---|---|---|
| 1º escrito | `def` | na definição, nada é calculado |
| 2º escrito | `demo_defaultdict_grupos` | na definição, nada é calculado |
| 3º escrito | `pares` | na definição, nada é calculado; na chamada, recebe a lista antes do corpo |
| 4º escrito | `: list[tuple[str, str]]` | na definição, nada é calculado |
| 5º escrito | `-> dict[str, list[str]]` | na definição, nada é calculado |
| 6º escrito | `grupos` | no corpo: o nome passa a apontar para o dicionário criado à direita |
| 7º escrito | `: dict[str, list[str]]` | nada é calculado |
| 8º escrito | `= defaultdict(list)` | primeiro no corpo: cria o dicionário vazio |
| 9º escrito | `for` | depois: uma volta para cada par |
| 10º escrito | `chave, valor` | em cada volta, depois de pegar o par |
| 11º escrito | `in pares` | em cada volta, primeiro: entrega o próximo par |
| 12º escrito | `grupos[chave]` | em cada volta, primeiro dentro do corpo: acha a lista |
| 13º escrito | `.append(valor)` | em cada volta, logo em seguida: acrescenta o produto |
| 14º escrito | `return` | por último, quando o `for` acabou |
| 15º escrito | `dict(grupos)` | imediatamente antes do `return` |

Uma volta, com `("fruta", "uva")`, anda nesta fila: `pares` entrega o par, `chave` fica `"fruta"`, `valor` fica `"uva"`, `grupos["fruta"]` abre uma lista vazia, `append` põe `"uva"` dentro. A volta acaba e o `for` pede o próximo par. O `return` espera todas as voltas.

| Volta | Par | `grupos` no fim da volta |
|---|---|---|
| 1 | `("fruta", "uva")` | `{"fruta": ["uva"]}` |
| 2 | `("fruta", "maçã")` | `{"fruta": ["uva", "maçã"]}` |
| 3 | `("cor", "azul")` | `{"fruta": ["uva", "maçã"], "cor": ["azul"]}` |

Na volta 2 a chave `fruta` já existe, então a lista é a mesma e a `maçã` entra no fim. Na volta 3, `cor` ainda não existe, então nasce outra lista. Aí o `dict` copia e o `return` entrega.

## A mesma função, em linhas separadas

```python
def demo_defaultdict_grupos(pares: list[tuple[str, str]]) -> dict[str, list[str]]:
    grupos: dict[str, list[str]] = defaultdict(list)
    for chave, valor in pares:
        lista = grupos[chave]
        lista.append(valor)
    copia = dict(grupos)
    return copia
```

`grupos`, `lista` e `copia` são as variáveis que a função cria.

| Linha | O que acontece |
|---|---|
| `grupos = defaultdict(list)` | cria o dicionário que abre uma lista vazia para chave nova |
| `for chave, valor in pares` | pega cada par da lista |
| `lista = grupos[chave]` | busca a lista daquela chave |
| `lista.append(valor)` | acrescenta o valor nessa lista |
| `copia = dict(grupos)` | copia os grupos para um dicionário comum |
| `return copia` | devolve a cópia |

## O que ficou claro

1. A casca da função é a mesma da [[demo_counter]]. O que muda é o meio: aqui o `defaultdict` agrupa, lá o `Counter` conta.
2. `pares` é o nome do parâmetro. `list` na anotação é o tipo. A lista chega pronta na chamada.
3. `list[tuple[str, str]]` é uma lista de pares. Cada par é uma tupla de duas strings. A leitura é de fora para dentro.
4. Nesta função, o primeiro texto da tupla é a categoria e o segundo é o produto. Quem faz essa separação é `for chave, valor in pares`.
5. A tupla se lê e não recebe `append`. A lista do dicionário é quem cresce.
6. `defaultdict(list)` abre a lista vazia na primeira vez da chave. Por isso o loop não testa `if chave not in grupos`.
7. No exemplo das palavras, a chave é `word[0]`, o primeiro caractere. O `append` guarda a palavra inteira.
8. `dict(grupos)` copia o resultado, e o `return` entrega essa cópia depois que o `for` terminou.
