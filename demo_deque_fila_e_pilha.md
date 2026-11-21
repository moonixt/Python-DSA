---
title: demo_deque_fila_e_pilha
date: 2026-11-21
tags:
  - python
  - deque
  - fila
  - pilha
aliases:
  - deque
  - FIFO
  - LIFO
related: "[[demo_defaultdict_grupos]]"
---

# demo_deque_fila_e_pilha

**1h 35min. 24 perguntas.** 21 nov 2026, 08:20–09:55. A função foi aberta em 20 nov, 18:13, e a noite entre as duas sessões não entra na conta. Dois comentários sobre tipagem, o pedido da analogia na skill e o pedido da nota também ficam de fora.

## Como as perguntas andaram

As primeiras perguntas testaram a regra da anotação numa função nova. O meio foi o mecanismo da fila. O fim foi um buraco básico de `for`, e a pergunta seguinte foi para a documentação, não para parar. O mapa das três funções está em [[Review]].

| Trabalho | Quantas | Onde apareceu |
|---|---|---|
| Destrava | 8 | `deque` da esquerda é a variável; frente, meio e fim; `v` seria o índice; `iterable` seria o `v`; `start` seria uma função |
| Confere | 7 | `defaultdict` dos dois lados funciona; a analogia do time e do autógrafo; a pilha repete a fila pelo fim |
| Leva | 9 | por que não uma lista; `enumerate` e `range`; onde ler parâmetros; tipagem e desempenho; a mesma função em TypeScript |

A última pergunta resumiu a função: a fila anota o `popleft`, a pilha faz o mesmo pelo `pop`. As 24 perguntas não ficaram espalhadas. Elas trocaram de assunto quando o anterior já sustentava o próximo.

Nota de estudo da função em `00_fase0_python_essentials.py`. A casca é a mesma de [[demo_counter]] e [[demo_defaultdict_grupos]]: `def`, nome, parâmetro com tipo, `->` com o tipo da saída, e o `return` no fim. Liga com [[Listas e dicionarios]].

```python
from collections import deque

def demo_deque_fila_e_pilha(valores: list[int]) -> tuple[list[int], list[int]]:
    """
    deque faz append/pop nas duas pontas em O(1).
    Usamos como fila (BFS) e como pilha (DFS / stack).
    """
    fila: deque[int] = deque()
    for v in valores:
        fila.append(v)  # entra no fim
    ordem_fila: list[int] = []
    while fila:
        ordem_fila.append(fila.popleft())  # sai da frente: FIFO

    pilha: deque[int] = deque()
    for v in valores:
        pilha.append(v)
    ordem_pilha: list[int] = []
    while pilha:
        ordem_pilha.append(pilha.pop())  # sai do fim: LIFO
    return ordem_fila, ordem_pilha
```

Chamada:

```python
demo_deque_fila_e_pilha([1, 2, 3])
# ([1, 2, 3], [3, 2, 1])
```

A mesma lista entra duas vezes. A fila devolve os números na ordem de chegada. A pilha devolve do último para o primeiro. O `return` entrega as duas listas juntas, numa tupla.

## Ordem da função

A ordem na função é: `def`, nome, `valores`, tipo da entrada, tipo da saída, montar a fila, esvaziar a fila pela frente, montar a pilha, esvaziar a pilha pelo fim, `return` das duas listas.

| Pedaço | O que é |
|---|---|
| `def` | palavra que abre a definição da função |
| `demo_deque_fila_e_pilha` | nome da função |
| `valores` | nome do parâmetro, a lista que entra |
| `: list[int]` | tipo dessa lista: números inteiros |
| `-> tuple[list[int], list[int]]` | tipo da saída: um par com duas listas de inteiros |
| `fila` | a variável da fila |
| `: deque[int]` | a anotação: um `deque` de inteiros. Nada é criado aqui |
| `= deque()` | a chamada que cria a fila vazia |
| `for v in valores` | percorre a lista. `v` é o próprio número, não o índice |
| `fila.append(v)` | coloca o número no fim |
| `ordem_fila: list[int] = []` | a lista vazia que anota a ordem da fila |
| `while fila` | repete enquanto a fila ainda tem número |
| `fila.popleft()` | tira o número da frente |
| `ordem_fila.append(...)` | anota esse número |
| `pilha = deque()` | outra estrutura, vazia, montada de novo |
| `pilha.append(v)` | coloca o número no fim |
| `pilha.pop()` | tira o número do fim |
| `return ordem_fila, ordem_pilha` | devolve as duas listas como um par |

Numa linha `nome: Tipo = Chamada()`, o nome antes dos dois pontos é a variável. O tipo depois dos dois pontos não cria o valor. A chamada depois do `=` cria. Em `fila: deque[int] = deque()`, os dois lados usam a palavra `deque`, e mesmo assim o primeiro é a anotação e o segundo é a chamada. Em `grupos: dict[str, list[str]] = defaultdict(list)`, os nomes diferem porque um `defaultdict` é um `dict`.

## Ferramentas

```python
from collections import deque
```

| Ferramenta | De onde vem | Papel nesta função | Documentação |
|---|---|---|---|
| `deque` | `collections` | cria a fila vazia, com duas pontas | [deque](https://docs.python.org/3/library/collections.html#collections.deque) |
| `append` | método do `deque` | põe o item no fim | [deque.append](https://docs.python.org/3/library/collections.html#collections.deque.append) |
| `popleft` | método do `deque` | tira o item da frente | [deque.popleft](https://docs.python.org/3/library/collections.html#collections.deque.popleft) |
| `pop` | método do `deque` | tira o item do fim | [deque.pop](https://docs.python.org/3/library/collections.html#collections.deque.pop) |

`deque()` não recebe número nenhum. Os parênteses vazios só constroem a estrutura. Com `[1, 2, 3]`, a fila fica `[1, 2, 3]` e `popleft` tira `1`, depois `2`, depois `3`. A pilha fica `[1, 2, 3]` e `pop` tira `3`, depois `2`, depois `1`.

## Analogia

Nas duas cenas, quem está na frente sai. A diferença é se o resto da fila dá um passo ou fica no lugar. A fila é Ana, Bruno, Caio, Duda. Ana é a frente.

| Cena | O que acontece | No código |
|---|---|---|
| Escolha do time | Ana sai, e Bruno passa a ser a frente sem ninguém andar. Bruno sai, e Caio passa a ser a frente. Caio e Duda ficam no próprio lugar | `deque` com `popleft` |
| Fila do autógrafo | Ana sai, e Bruno, Caio e Duda dão um passo à frente. Bruno sai, e Caio e Duda dão outro passo | lista com `pop(0)` |

Numa lista, os itens ficam em posições numeradas. Tirar o da frente obriga cada um dos outros a mudar de número. No `deque`, a frente é uma marca: `popleft` avança essa marca e o resto fica onde está.

Antes de `popleft()`, em `deque([1, 2, 3, 4])`:

| Lugar | Número |
|---|---|
| frente | `1` |
| entre as pontas | `2` |
| entre as pontas | `3` |
| fim | `4` |

Depois, o `1` saiu. O `2` não andou: passou a ser a frente. O `3` e o `4` ficaram no lugar.

| Lugar | Número |
|---|---|
| frente | `2` |
| entre as pontas | `3` |
| fim | `4` |

`pop()` tira o `4`, na ponta direita.

## O `for` e o `while`

O `for` percorre `valores` e coloca cada número no fim da fila. `ordem_fila` é outra lista, vazia, onde a ordem de saída é anotada. O `while` repete enquanto ainda houver alguém na fila.

```python
for v in valores:
    fila.append(v)
ordem_fila: list[int] = []
while fila:
    ordem_fila.append(fila.popleft())
```

| Volta do `while` | Sai da frente | `fila` depois | `ordem_fila` depois |
|---|---|---|---|
| 1 | `1` | `[2, 3]` | `[1]` |
| 2 | `2` | `[3]` | `[1, 2]` |
| 3 | `3` | `[]` | `[1, 2, 3]` |

A fila ficou vazia, então o `while` para. A pilha é enchida de novo, do mesmo jeito, e esvaziada pelo fim.

| Etapa | Fila | Pilha |
|---|---|---|
| Criar | `fila = deque()` | `pilha = deque()` |
| Encher com `append` | `[1, 2, 3]` | `[1, 2, 3]` |
| Tirar | `popleft`: da frente | `pop`: do fim |
| Anotar | `ordem_fila` fica `[1, 2, 3]` | `ordem_pilha` fica `[3, 2, 1]` |

FIFO: o primeiro que entra é o primeiro que sai. LIFO: o último que entra é o primeiro que sai. A fila é a estrutura de uma busca em largura. A pilha é a estrutura de uma busca em profundidade.

## `v` é o item

Em `for v in valores`, `v` é o próprio número. Com `[1, 2, 3]`, as voltas entregam `1`, depois `2`, depois `3`. O índice só aparece se o `for` pedir a posição.

`enumerate` entrega a posição e o valor juntos. `range(len(valores))` entrega só a posição, e `valores[i]` busca o número.

| Volta | `enumerate` entrega | `range(len(valores))` entrega | `valores[i]` |
|---|---|---|---|
| 1 | `(0, 1)` | `0` | `1` |
| 2 | `(1, 2)` | `1` | `2` |
| 3 | `(2, 3)` | `2` | `3` |

`iterable`, na assinatura de `enumerate`, é a lista inteira. `v` é um item dessa lista. `start` é um parâmetro de `enumerate`, não uma função: `start=1` faz a contagem começar em `1`. A assinatura fica em [enumerate](https://docs.python.org/3/library/functions.html#enumerate). As funções embutidas estão em [Built-in Functions](https://docs.python.org/3/library/functions.html).

## Ordem de execução

A tabela seguinte é a ordem de execução. As linhas continuam na ordem da leitura.

| Ordem na linha | Pedaço | Quando roda |
|---|---|---|
| 1º escrito | `def` e o nome | na definição, nada é calculado |
| 2º escrito | `valores: list[int]` | na chamada, recebe `[1, 2, 3]` antes do corpo |
| 3º escrito | `-> tuple[list[int], list[int]]` | na definição, nada é calculado |
| 4º escrito | `: deque[int]` | nada é calculado |
| 5º escrito | `fila = deque()` | primeiro no corpo: cria a fila vazia |
| 6º escrito | `for v in valores` | uma volta para cada número |
| 7º escrito | `fila.append(v)` | em cada volta: o número entra no fim |
| 8º escrito | `ordem_fila = []` | cria a lista vazia que vai receber a saída da fila |
| 9º escrito | `while fila` | repete enquanto a fila ainda tem número |
| 10º escrito | `fila.popleft()` | em cada volta do `while`, primeiro: tira o da frente |
| 11º escrito | `ordem_fila.append(...)` | em seguida: guarda esse número |
| 12º escrito | `pilha = deque()` | a fila já acabou: cria a pilha vazia |
| 13º escrito | `pilha.append(v)` | enche a pilha com `[1, 2, 3]` de novo |
| 14º escrito | `while pilha` | repete enquanto a pilha ainda tem número |
| 15º escrito | `pilha.pop()` | em cada volta, primeiro: tira o do fim |
| 16º escrito | `ordem_pilha.append(...)` | em seguida: guarda esse número |
| 17º escrito | `return ordem_fila, ordem_pilha` | por último: devolve o par |

`popleft()` roda antes do `append` que guarda o número, porque está dentro dos parênteses. O mesmo vale para `pilha.pop()`.

## A mesma função, em linhas separadas

```python
def demo_deque_fila_e_pilha(valores: list[int]) -> tuple[list[int], list[int]]:
    fila: deque[int] = deque()
    for v in valores:
        fila.append(v)
    ordem_fila: list[int] = []
    while fila:
        saiu = fila.popleft()
        ordem_fila.append(saiu)

    pilha: deque[int] = deque()
    for v in valores:
        pilha.append(v)
    ordem_pilha: list[int] = []
    while pilha:
        saiu = pilha.pop()
        ordem_pilha.append(saiu)
    return ordem_fila, ordem_pilha
```

`deque` vem de `collections`. `fila`, `pilha`, `ordem_fila`, `ordem_pilha` e `saiu` são as variáveis que a função cria.

| Linha | O que acontece |
|---|---|
| `fila = deque()` | cria a fila vazia |
| `fila.append(v)` | número entra no fim |
| `saiu = fila.popleft()` | número sai da frente |
| `ordem_fila.append(saiu)` | guarda esse número |
| `pilha = deque()` | cria a pilha vazia |
| `pilha.append(v)` | número entra no fim de novo |
| `saiu = pilha.pop()` | número sai do fim |
| `ordem_pilha.append(saiu)` | guarda esse número |
| `return ordem_fila, ordem_pilha` | devolve as duas listas |

## O que ficou claro

1. `fila` é a variável. `: deque[int]` é a anotação e não cria a fila. `deque()` cria a fila vazia.
2. O mesmo nome nos dois lados do `=` continua sendo dois papéis. Nomes diferentes também funcionam quando o valor criado cabe na anotação, como `dict` na esquerda e `defaultdict(list)` na direita.
3. A lista tira da frente deslocando todo mundo. O `deque` só avança a marca da frente.
4. O `for` lê `valores`. `v` é o item, não o índice. O `while` é um segundo loop e esvazia a fila.
5. `ordem_fila` anota quem saiu da frente. `ordem_pilha` anota quem saiu do fim. A pilha é enchida de novo, do mesmo jeito.
6. FIFO é a ordem `[1, 2, 3]`. LIFO é a ordem `[3, 2, 1]`. O `return` junta as duas listas numa tupla.
7. A anotação não muda a velocidade. Ela mostra o formato antes do corpo.
