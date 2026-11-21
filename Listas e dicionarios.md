A ordem de uma função python é:

nome da função, parâmetro dela, tipo do parâmetro, tipo da saida.

Exemplo: 
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
