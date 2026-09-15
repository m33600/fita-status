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

## Limites

- A página mostra o que está gravado no dweet.cc, não o que a fita está
  exibindo: se a fita estiver desligada ou sem WiFi, a página não percebe.
- O dweet.cc apaga o valor depois de 24 h sem gravação; a página então mostra
  "sem status" até alguém tocar numa cor.
