---
name: break-note
description: >-
  Save a break study note as an Obsidian markdown file in the Tech Research
  vault and update the learning trail. Use when the user asks to create the
  .md, save the breakdown to Obsidian, or write the note for a function they
  just learned with break.
---

# Break note

Turn the current `break` into one study note. Reply in the user's language. Write the file. Do not paste the note back into the chat.

## Where

Vault: `/home/arch/Clones/Tech Research`

File name: the function name plus `.md`, in the vault root, as in `demo_counter.md`. If that file already exists, update it in place.

Write the file directly. Do not pass the body through `obsidian create content=`.

## Source

Use the `break` already done in this conversation: source order, imported tools, execution order, and the separated form. If there is no `break` yet, do that breakdown first, then write the note from it.

Keep a fact only when it came from that breakdown or from a question the user asked about this function. "O que ficou claro" is one short sentence per conclusion, in the order the user reached it.

## Note shape

Frontmatter:

```yaml
---
title: nome_da_funcao
date: YYYY-MM-DD
tags:
  - linguagem
  - assunto
aliases:
  - ferramenta importada
related: "[[nota relacionada]]"
---
```

Quote wikilinks in YAML. Leave a blank line before every table.

1. Title, then one bold line with the hours and the number of questions. Count from the first question about this function to the last one before the note request. Use the question timestamps. Leave out overnight gaps, skill requests, and the note request itself, and say so.
2. `## Como as perguntas andaram`. The subject is the person, not the questions. Three sentences: what they could already read, what was still missing, what they did without being asked. Link `[[Como as perguntas andaram]]`.
3. One sentence naming the source file. Wikilink a sibling note when one exists, such as `[[demo_counter]]` and `[[Listas e dicionarios]]`.
4. The function in a code block, import included.
5. A call with concrete values and the returned value in a comment.
6. `## Ordem da função`, the source-order sentence, then `Pedaço` | `O que é`.
7. `## Ferramentas`, the import line, then `Ferramenta` | `De onde vem` | `Papel nesta função` | `Documentação`. The link is the official docs URL from the `break` skill. Follow with the concrete walk of that tool.
8. `## Analogia`, the two scenes from the `break` and the table `Cena` | `O que acontece` | `No código`. Keep the shared fact in one sentence above the table.
9. One section per extra idea the user actually asked about, with a small table.
10. `## Ordem de execução`, then `Ordem na linha` | `Pedaço` | `Quando roda`. If the function loops, add the table of each lap and the value at the end of the lap.
11. `## A mesma função, em linhas separadas`, the code, then `Linha` | `O que acontece`.
12. `## O que ficou claro`, a numbered list.

## Trail

Update `Como as perguntas andaram.md` in the same vault. The subject is the person moving from one function to the next. Questions are only the trace.

Add or replace one row in the opening table: function link, what they could already do, what was still missing, what they did without being asked.

Add or replace one section for this function. Say what they could read on arrival, what stayed opaque, and what they started doing alone. Include the hours and the question count in one line at the end of that section. Name a real gap when one showed up late, and say whether they left it or turned it into the next step.

Rewrite `## O que mudou na pessoa` so it still describes the whole trail after this function. Do not score. Do not turn the trail back into a count of question types.
