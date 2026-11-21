---
title: Como as perguntas andaram
date: 2026-11-21
tags:
  - estudo
  - python
aliases:
  - evolução
related: "[[demo_counter]]"
---

# Como as perguntas andaram

O assunto aqui é a leitura, de uma função para a outra. As perguntas ficam como rastro dessa leitura. As notas são [[demo_counter]], [[demo_defaultdict_grupos]] e [[demo_deque_fila_e_pilha]].

| Momento | O que já dava para fazer | O que ainda faltava | O que passou a acontecer sozinho |
|---|---|---|---|
| [[demo_counter]] | Ver a função e perguntar o que ela conta | Ver onde a linha começa, onde termina e como os pedaços se falam | Separar nome, parâmetro, tipo e `return`. Reconhecer o `Counter` como import |
| [[demo_defaultdict_grupos]] | Ler a casca igual à da função anterior | Tupla, e a ordem do `for` quando a concentração cai | Sair do arquivo, ler a documentação e voltar com o agrupamento certo |
| [[demo_deque_fila_e_pilha]] | Comparar a anotação desta função com a do `grupos` | `for` e `while`, e a diferença entre item e índice | Inventar a analogia do time e do autógrafo, e resumir a fila e a pilha no fim |

## Counter

Na primeira manhã a linha era um bloco só. A leitura pedia cada pedaço nomeado: o que entra, o que a seta faz, o que o `return` faz, o que roda primeiro. Quatro voltas no `->` não foram a mesma dúvida. A primeira achava que a seta convertia a lista. A última já sabia que a seta é o tipo da saída e o `return` é quem entrega o valor.

No fim dessa função, a versão em duas linhas fez sentido, e o `Counter` deixou de ser um nome solto. À tarde, a frase foi esta: nas próximas funções a leitura está melhor porque a estrutura é parecida. Isso se confirmou na função seguinte. `def`, parâmetro, `->` e `return` não foram perguntados de novo.

Conceitos que ficaram:

- Na lista, a identidade é a posição. No dicionário, a identidade é a chave.
- `->` anuncia o tipo da saída. `return` entrega o valor.
- A leitura vai da esquerda para a direita. A execução entra no parêntese de dentro.
- `Counter` vem de `collections`. A variável é quem guarda o resultado.
- `list[str]` e `dict[str, int]` são anotações. O Python executa pelos valores.

2h 22min. 15 perguntas. Quase todas para conseguir ler uma linha.

## defaultdict

A função foi pedida inteira, no formato do breakdown. A casca já estava lida. O tempo foi para o que era novo: uma lista de pares, o que é tupla, se o par é categoria e produto, se dá para inserir.

A tupla como categoria e produto estava certa para esta função. A pergunta seguinte, se uma lista também servia, foi um teste do limite, não uma repetição. O `for` ainda custou um reforço. A concentração tinha caído, e o reforço foi pedido com essa clareza.

Depois disso a leitura saiu do chat. A documentação do `defaultdict` foi aberta, e a volta trouxe o exemplo certo: a palavra entra na lista da primeira letra. Essa foi a primeira vez em que a fonte foi buscada e a conclusão veio pronta.

Conceitos que ficaram:

- `list[tuple[str, str]]` é uma lista, e cada item é uma tupla de duas strings.
- A tupla se lê e permanece com os itens com que nasceu. Quem cresce é a lista do dicionário.
- Nesta função, o primeiro texto é a categoria e o segundo é o produto.
- `defaultdict(list)` abre uma lista vazia quando a chave ainda não existe.
- A esquerda pode dizer `dict` e a direita chamar `defaultdict(list)`, porque um `defaultdict` é um `dict`.

1h 14min. 13 perguntas. Nenhuma sobre a casca da função.

## deque

A função parecia a mais complexa, e a primeira comparação foi com uma regra já sua: no `grupos` a esquerda diz `dict` e a direita chama `defaultdict`. No `deque` os dois lados têm o mesmo nome. Essa diferença não estava no texto. Foi percebida.

O mecanismo da fila entrou pela cena, não pela definição. A escolha do time e a fila do autógrafo foram propostas, e os dois lados correspondiam a `popleft` e a `pop(0)`. Quem estudava passou a explicar o código.

O buraco do `for` apareceu tarde, com nome: a falha era não ter separado item e índice. A leitura não parou nesse buraco. A pergunta seguinte foi o que é `enumerate`, depois `range`, depois onde os parâmetros das funções embutidas ficam escritos. A tipagem, o desempenho e a versão em TypeScript foram o mesmo movimento: levar a função para fora do arquivo.

A última formulação fechou o que a função faz. A ordem da fila recebe quem sai da frente. A pilha faz o mesmo pelo fim.

Conceitos que ficaram:

- `fila` é a variável. `: deque[int]` é a anotação. `deque()` cria a fila vazia.
- Tirar da frente numa lista desloca o resto. No `deque`, a marca da frente avança e os outros ficam no lugar.
- `for v in valores`: `v` é o item. O índice aparece com `enumerate` ou `range(len(...))`.
- `iterable` é a sequência inteira. `start` é um parâmetro de `enumerate`, e o padrão é `0`.
- A fila é FIFO, a pilha é LIFO. O `return` junta as duas listas numa tupla.
- A anotação não deixa a função mais rápida.

1h 35min. 24 perguntas. O número é maior porque a função tem dois caminhos e porque a leitura já alcançava documentação, tipo e outra linguagem. A noite entre a abertura e a manhã seguinte não entra nessa conta.

## Conceitos que viajam

Estes não ficaram presos na função em que nasceram.

| Conceito | Onde nasceu | Onde voltou a servir |
|---|---|---|
| Anotação não cria o valor | `Counter` | `grupos: dict = defaultdict(list)` e `fila: deque[int] = deque()` |
| Import é a ferramenta, variável guarda o resultado | `Counter` | `defaultdict` e `deque` já foram lidos assim |
| Tupla é um pacote que se lê | `defaultdict` | O `return` da fila entrega duas listas nesse pacote |
| Item não é índice | `deque` | `enumerate` e `range` passaram a ter lugar |
| Documentação tem a assinatura do parâmetro | `deque` | `start=0` em `enumerate` foi lido na página, não adivinhado |

## O que mudou na pessoa

No começo, a linha precisava ser desmontada por outra pessoa. No `defaultdict`, a casca já era lida e a documentação passou a ser uma fonte. No `deque`, a comparação entre funções, a analogia e o resumo final saíram sem serem pedidos.

O que não sumiu: um pedaço básico pode continuar opaco mesmo quando a função grande já faz sentido. O `for` estava nesse lugar. Ele foi nomeado e virou o caminho até a documentação, em vez de desfazer o que já tinha sido entendido na fila.
