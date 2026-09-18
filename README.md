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

## Título da página (opcional)

**https://m33600.github.io/fita-status/#&lt;nome-da-fita&gt;:&lt;rótulo&gt;**

Depois do nome da fita, um `:` e um rótulo (ex. `Posto 7`, com espaço
codificado como `%20` ou `+`) definem o título da aba e o título na página —
sem isso, fica o genérico "Fita de status". Como o nome da fita nunca tem
`:`, cortar no primeiro `:` do link não tem ambiguidade. O
[painel](painel.html) já gera o link assim, usando o rótulo de cada posto.

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

## Painel de todos os postos

**https://status.settima.com.br/painel.html#&lt;posto1&gt;=&lt;rótulo1&gt;|&lt;posto2&gt;=&lt;rótulo2&gt;|…**

Mostra, num grid, a cor confirmada de vários postos ao mesmo tempo (pensado para
começar com 10). Cada cartão do grid é um link para a página de trocar a cor
(`index.html#<nome-da-coisa>:<rótulo>`) daquele posto — não existe um "teclado"
separado por posto: é a mesma página de sempre, cada posto com o seu nome (e o
rótulo, que vira o título da página nela) depois do `#`.

Assim como no `index.html`, **o nome de cada coisa só vive no link**, nunca no
repositório. Um posto sem coisa ainda (rótulo sem nome depois do `=`) aparece como
"ainda não configurado", sem tentar ler nada.

Sem nenhum posto no link, a página abre um formulário para montar a lista (nome da
coisa + rótulo, uma linha por posto) e gera o link — inclusive para editar um painel
que você já tem, clicando em "editar postos".

Cada posto configurado também mostra um **QR code**, gerado no próprio navegador (a
biblioteca [`qrcodegen.js`](https://www.nayuki.io/page/qr-code-generator-library), de
domínio público, fica neste repositório — nada é gerado por um serviço de terceiro, o
que também evitaria mandar o nome da coisa para fora). O QR aponta direto para o
teclado daquele posto. Quem for operar uma fita leva o celular até o painel (no
tablet ou no computador), aponta a câmera pro QR do posto certo e o celular abre o
teclado já naquele posto — sem precisar mandar link por mensagem. Tocar no QR do
próprio painel amplia ele na tela, para facilitar escanear de mais longe.

## Limites

- O dweet.cc apaga cada coisa depois de 24 h sem gravação. A confirmação da fita
  se renova sozinha; o status pedido, não — se ninguém tocar numa cor por 24 h e
  a fita reiniciar, ela fica sem status até o próximo toque.
- O `?api=` no endereço (para testar por um proxy local) só funciona com a
  página aberta em `127.0.0.1`; publicada, ela fala sempre com o dweet.cc.
