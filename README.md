# fita-status

Página para trocar, de qualquer lugar, a cor da fita de LED de status da fábrica.

**https://m33600.github.io/fita-status/#&lt;nome-da-fita&gt;**

A página grava um número no [dweet.cc](https://dweet.cc) e a fita (firmware
`fita-led-status`, no repositório factory) lê esse número a cada 3 s:

| Botão | Valor |
|---|---|
| Verde | 1 |
| Amarelo | 2 |
| Vermelho | 3 |
| Apagar | 0 |

Teclas `1`, `2`, `3` e `0` fazem o mesmo que os botões.

## O nome da fita fica fora do repositório

Quem souber o nome da fita consegue mudar a cor dela. Por isso ele não está em
nenhum arquivo daqui: vai no link, depois do `#`. O navegador não envia essa
parte do endereço ao GitHub, então ela só existe no link que você compartilha.

Mandou o link para alguém que não deveria ter? Troque o `DWEET_COISA` no
`secrets.h` do firmware, regrave a placa e envie o link novo.

## Confirmação da fita

A fita (firmware v0.3 ou mais novo) grava o que está mostrando em
`<nome-da-fita>-fita`: na hora em que a cor muda e depois a cada 30 s. A página
lê essa coisa e mostra:

- **✓ confirmado pela fita há X s** — a fita está ligada e mostrando essa cor;
- **pedido: Amarelo, aguardando a fita…** — o clique chegou ao dweet.cc, mas a
  fita ainda não aplicou (normal por até ~5 s);
- **fita sem sinal há X min** — nenhuma confirmação há mais de 75 s: a fita está
  desligada ou sem internet, e a cor mostrada é a última que ela confirmou.

O pedido fica gravado: se a fita estiver fora do ar, ela aplica quando voltar.

## Limites

- O dweet.cc apaga cada coisa depois de 24 h sem gravação. A confirmação da fita
  se renova sozinha; o status pedido, não — se ninguém tocar numa cor por 24 h e
  a fita reiniciar, ela fica sem status até o próximo toque.
- O `?api=` no endereço (para testar por um proxy local) só funciona com a
  página aberta em `127.0.0.1`; publicada, ela fala sempre com o dweet.cc.
