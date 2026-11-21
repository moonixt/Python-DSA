---
title: demo_counter
date: 2026-11-20
tags:
  - python
  - dicionario
  - counter
aliases:
  - Counter
  - breakdown demo_counter
related: "[[Listas e dicionarios]]"
---

# demo_counter

**2h 22min. 15 perguntas.** 20 nov 2026, 08:16–10:38. O intervalo vai da primeira pergunta sobre esta função até a última antes do pedido da nota. Pedidos de skill, extensão e da própria nota não entram na conta.

## Como as perguntas andaram

Cada pergunta fez um trabalho. Destrava: nomeia um mecanismo errado e a correção tem onde pousar. Confere: repete com as próprias palavras. Leva: usa a resposta num pedaço novo. O mapa das três funções está em [[Review]].

| Trabalho | Quantas | Onde apareceu                                                                                       |
| -------- | ------- | --------------------------------------------------------------------------------------------------- |
| Destrava | 6       | conta letra ou palavra; `->` converte; `Counter` é variável; os valores cabem dentro de `list[str]` |
| Confere  | 7       | ordem da assinatura, o que o `return` devolve, `str` e `int` são opcionais, lista fixa com `=`      |
| Leva     | 2       | a ordem de execução, de dentro para fora; a mesma função em duas linhas                             |

O `->` foi perguntado quatro vezes, e cada vez o corte ficou mais fino: conversão, depois a lista já contada, depois o nome da seta, depois a seta ao lado do `return`. A pergunta não girava em falso. Nas funções seguintes, `->` não voltou.

Nota de estudo da função em `00_fase0_python_essentials.py`. Liga com [[Listas e dicionarios]].

```python
from collections import Counter

def demo_counter(palavras: list[str]) -> dict[str, int]:
    """Conta ocorrências. Equivale a um dict[str, int] atualizado no loop."""
    return dict(Counter(palavras))
```

Chamada:

```python
demo_counter(["gato", "cão", "gato"])
# {"gato": 2, "cão": 1}
```

Cada string inteira vira chave. O `int` é quantas vezes ela apareceu. O `Counter` não abre a palavra para contar letras. Isso só aconteceria se a entrada fosse uma string só, porque uma string é uma sequência de caracteres:

```python
Counter("banana")  # {"b": 1, "a": 3, "n": 2}
```

> [!tip] Posição ou identidade
> Na lista, a ordem é a identidade: `palavras[0]` e `palavras[2]` são dois itens, mesmo os dois sendo `"gato"`. No dicionário, a chave é a identidade: `contagem["gato"]` aponta para a palavra, e o `int` ao lado é a contagem. O índice da lista some nessa transformação.

## Ordem da assinatura

A ordem nessa linha é: `def`, nome, parâmetro, tipo do parâmetro, tipo do retorno.

```python
def demo_counter(palavras: list[str]) -> dict[str, int]:
```

| Pedaço | O que é |
|---|---|
| `def` | palavra que abre a definição da função |
| `demo_counter` | nome da função |
| `palavras` | nome do parâmetro, o valor que entra |
| `: list[str]` | tipo desse parâmetro: uma lista de strings |
| `-> dict[str, int]` | tipo do que a função devolve: um dicionário com chave string e valor int |

`list[str]` e `dict[str, int]` são anotações de tipo. Os colchetes dizem o que vai dentro: strings na lista, e no dicionário a chave é `str` e o valor é `int`.

## O que é `->`

`->` indica o tipo da saída. O `return` envia o valor dessa saída. Os dois falam da mesma porta de saída, cada um no seu papel.

| Pedaço                | Papel                                                                      |
| --------------------- | -------------------------------------------------------------------------- |
| `palavras: list[str]` | a entrada: uma lista de strings                                            |
| `-> dict[str, int]`   | a etiqueta da saída: "vai sair um dicionário com chave string e valor int" |
| `return dict(...)`    | a saída de verdade: monta esse dicionário e devolve para quem chamou       |

A seta fica na primeira linha e o Python não executa nada nela. Quem chama a função lê a seta para saber o formato do resultado. O `return` coloca `{"gato": 2, "cão": 1}` na mão de quem chamou.

`-> dict` anuncia o tipo. A conversão acontece no `dict(...)` do `return`.

| Pedaço | O que faz |
|---|---|
| `-> dict[str, int]` | etiqueta: "o resultado é um dicionário" |
| `Counter(palavras)` | lê a lista e conta cada string |
| `dict(...)` | pega essa contagem e monta um dicionário |

## As tipagens são opcionais

`list[str]` e `dict[str, int]` são anotações. O interpretador executa a função pelos valores que chegam. Sem as anotações, a função continua igual. O Python não preenche a anotação no lugar do que foi apagado.

```python
def demo_counter(palavras):
    contagem = Counter(palavras)
    return dict(contagem)
```

| Anotação | O que nomeia |
|---|---|
| `list[str]` | a entrada é uma lista, e cada item é string |
| `dict[str, int]` | a saída é um dicionário, chave string e valor int |

Com `["gato", "cão", "gato"]`, a chave sai `str` e o valor sai `int` porque a lista tem palavras e o `Counter` soma quantas vezes cada uma aparece.

## O return, nas duas ordens

```python
return dict(Counter(palavras))
```

A ordem na linha, da esquerda para a direita, é: `return`, `dict(...)`, `Counter(palavras)`.

| Pedaço              | O que é                                   |
| ------------------- | ----------------------------------------- |
| `return`            | devolve o valor para quem chamou a função |
| `dict(...)`         | copia a contagem para um dicionário comum |
| `Counter(palavras)` | conta cada string da lista                |

A tabela seguinte é a ordem de execução. As linhas continuam na ordem da leitura. A coluna `Quando roda` diz o momento em que cada pedaço roda.

| Ordem na linha | Pedaço | Quando roda |
|---|---|---|
| 1º escrito | `return` | por último: só devolve o que os parênteses já produziram |
| 2º escrito | `dict(...)` | no meio: espera o `Counter` terminar |
| 3º escrito | `Counter(palavras)` | primeiro: é o parêntese mais de dentro |

O Python entra no parêntese mais interno, sobe um nível e só então chega na palavra que está à esquerda.

Com `["gato", "cão", "gato"]`:

1. `Counter(palavras)` conta e entrega `gato` 2, `cão` 1.
2. `dict(...)` copia essa contagem para um dicionário.
3. `return` devolve `{"gato": 2, "cão": 1}` e a função termina.

## A função inteira, na ordem de execução

| Ordem | Pedaço | Lugar | Recebe | Entrega |
|---|---|---|---|---|
| 1 | `demo_counter(...)` | fora, quem chama | a lista `["gato", "cão", "gato"]` | essa lista para o parâmetro |
| 2 | `def demo_counter` | começo da definição | o nome da função | a porta de entrada aberta |
| 3 | `palavras: list[str]` | entrada | a lista | a lista guardada em `palavras`, cada item é `str` |
| 4 | `-> dict[str, int]` | etiqueta da saída | nenhum valor | o aviso do formato: chave `str`, valor `int` |
| 5 | `Counter(palavras)` | meio | a lista em `palavras` | a contagem: `gato` 2, `cão` 1 |
| 6 | `dict(...)` | meio | essa contagem | o dicionário `{"gato": 2, "cão": 1}` |
| 7 | `return` | fim | esse dicionário | o mesmo dicionário para quem chamou. A função termina |

A chamada entrega a lista, `palavras` segura a lista, o `Counter` lê essa lista, o `dict` copia a contagem, e o `return` devolve a cópia.

## A mesma função, em linhas separadas

```python
def demo_counter(palavras: list[str]) -> dict[str, int]:
    contagem = Counter(palavras)
    return dict(contagem)
```

| Linha                          | O que acontece                 |
| ------------------------------ | ------------------------------ |
| `contagem = Counter(palavras)` | lê a lista e guarda a contagem |
| `return dict(contagem)`        | copia essa contagem e devolve  |

## Ferramentas

```python
from collections import Counter, defaultdict, deque
```

| Ferramenta | De onde vem | Papel nesta função | Documentação |
|---|---|---|---|
| `Counter` | `collections` | percorre a lista e monta a contagem: cada string vira chave, o `int` é quantas vezes apareceu | [Counter](https://docs.python.org/3/library/collections.html#collections.Counter) |
| `dict` | embutido do Python | copia essa contagem para um dicionário comum | [dict](https://docs.python.org/3/library/stdtypes.html#dict) |

`Counter` é a ferramenta que o `import` trouxe. `contagem` é a variável que a função cria. A contagem precisa receber `palavras`. Sem isso, não há o que contar e sai um dicionário vazio.

A lista chega pronta. Pode ser fixa:

```python
demo_counter(["gato", "cão", "gato"])
```

O loop citado no docstring está dentro do `Counter`. Ele percorre a lista que já chegou e soma 1 para cada palavra. Escrito à mão:

```python
def demo_counter(palavras: list[str]) -> dict[str, int]:
    contagem: dict[str, int] = {}
    for palavra in palavras:
        contagem[palavra] = contagem.get(palavra, 0) + 1
    return contagem
```

## Lista fixa no parâmetro

A lista fixa fica depois do `=`, entre colchetes. O `list[str]` continua só como o tipo.

```python
def demo_countercopy(palavras: list[str] = ["gato", "cão", "gato"]) -> dict[str, int]:
    return dict(Counter(palavras))
```

| Pedaço | O que é |
|---|---|
| `palavras` | nome do parâmetro |
| `: list[str]` | tipo desse parâmetro |
| `= ["gato", "cão", "gato"]` | valor fixo, usado quando a chamada não manda outra lista |

`demo_countercopy()` usa essa lista. `demo_countercopy(["sol", "sol"])` usa a lista da chamada.

Criar a lista dentro da função, sem parâmetro:

```python
def demo_countercopy() -> dict[str, int]:
    palavras: list[str] = ["gato", "cão", "gato"]
    contagem = Counter(palavras)
    return dict(contagem)
```

`list[str]['gato', 'cão', 'gato']` deixa as palavras dentro da anotação. O Python guarda isso como texto do tipo e não monta a lista. O `=` sozinho não resolve: os valores precisam sair dos colchetes do tipo e formar a lista depois do `=`.

## A conversa, na ordem em que ficou clara

1. A função conta strings inteiras da lista. O `int` é a quantidade, não um caractere.
2. Na lista, o que se pensa primeiro é o índice, a posição. No dicionário, o equivalente é a chave, a identidade do item. No `Counter`, a pergunta é "qual item se repete?".
3. A assinatura se lê assim: `def`, nome, parâmetro, tipo do parâmetro, `->`, tipo do retorno.
4. O `return dict(Counter(palavras))` devolve um dicionário comum. O `Counter` conta. O `dict(...)` copia para o tipo que a seta anuncia.
5. Declarar `str` e `int` no retorno é opcional. Essa anotação descreve o dicionário que sai, não o parâmetro. O parâmetro é `palavras: list[str]`.
6. `-> dict` é a etiqueta da saída. A lista vira dicionário no `dict(...)`, depois da contagem.
7. A lista chega pronta, o `Counter` conta, o `dict(...)` entrega a contagem.
8. `->` é o indicador do tipo da saída. O `return` é quem envia o valor.
9. A tabela grande segue a ordem de execução. Na linha, `return` está escrito primeiro. Na execução, o parêntese de dentro roda primeiro.
10. Dá para separar em `contagem = Counter(palavras)` e `return dict(contagem)`. Fica a mesma função, mais fácil de ler.
11. `Counter` não é uma variável inventada na função. É a ferramenta importada de `collections`.
12. Apagar `[str]` e `[int]` não faz o interpretador "assumir" a anotação. Ele usa os valores que chegaram.
13. Lista fixa se escreve `palavras: list[str] = ["gato", "cão", "gato"]`, ou `palavras = ["gato", "cão", "gato"]` dentro da função.
