# Ateliê do Automóvel

Site institucional do Ateliê do Automóvel 191, estética automotiva em
Ubatuba/SP — polimento, higienização e detailing.

**Em desenvolvimento** · [Ver no ar](https://atelie-estetica.netlify.app)

> A versão publicada na Netlify é provisória, usada para validação com o
> cliente. Ela está com `noindex` para não competir no Google com o endereço
> oficial da empresa.

---

## Sobre o projeto

Página única, escura, com identidade em preto e dourado. O objetivo é
mostrar o serviço e levar a pessoa para o WhatsApp.

Projeto feito do zero: layout, código, otimização de mídia e publicação.

## Decisões técnicas

**Sem framework.** HTML, CSS e JavaScript puro. Uma página, sem build e sem
dependência de pacote.

**Mídia em arquivos separados, não embutida.** A primeira versão trazia a
logo, as fotos e o vídeo de apresentação embutidos no HTML em base64 — o
`index.html` tinha 11 MB e o navegador precisava baixar tudo antes de
desenhar qualquer coisa. Extraí cada item para `img/` e `video/`:

| | antes | depois |
|---|---|---|
| `index.html` | 11 MB | 31 KB |

Três ganhos concretos:

- A página aparece de imediato, em vez de esperar o vídeo terminar de baixar
- A logo estava repetida quatro vezes dentro do HTML, 222 KB cada; agora é
  um arquivo só, que o navegador guarda em cache e reaproveita
- O `preload="metadata"` do vídeo passou a funcionar de verdade: os 6,9 MB
  só descem quando a pessoa aperta o play

**Fontes auto-hospedadas.** Poppins nos títulos e Inter no texto, servidas em
`.woff2` do próprio site, em vez de virem do Google Fonts. Baixei apenas o
subconjunto `latin`, que cobre o português — o `latin-ext` existe para o
leste europeu e não serve aqui.

Ganho de rede: antes o navegador precisava resolver o DNS de
`fonts.googleapis.com`, abrir conexão, baixar um CSS, descobrir dentro dele
os endereços em `fonts.gstatic.com`, abrir uma segunda conexão e só então
pedir as fontes. Duas viagens a servidores de terceiros antes da primeira
letra. Agora os arquivos vêm na conexão que já está aberta.

Carrego só os pesos que a página usa — Poppins 600/700/800 e Inter
400/600/700. O link antigo pedia dois pesos que nenhuma regra de CSS usava.

Um deles entrou novo: o selo "mais escolhido" pede Inter 700, e o Google
Fonts nunca serviu esse peso ao site. Quando falta o peso pedido, o
navegador não desiste — ele engorda a letra sozinho, esticando os traços. O
resultado é um negrito borrado, diferente do que o tipógrafo desenhou.

**Imagens em WebP, com `width` e `height` declarados.** Cada imagem foi
convertida no tamanho em que realmente aparece na tela, não no tamanho do
arquivo original:

| | antes | depois |
|---|---|---|
| logo | `logo.png` 222 KB | `logo.webp` 24 KB |
| foto principal | `hero.jpg` 122 KB | `hero.webp` 69 KB |
| capa do vídeo | `video-poster.jpg` 137 KB | `video-poster.webp` 71 KB |
| favicon | usava a logo de 222 KB | `icon-32.png` 3 KB |
| **total** | **493 KB** | **177 KB** |

As dimensões declaradas em cada tag permitem ao navegador reservar o espaço
antes de a imagem chegar, em vez de empurrar o conteúdo para baixo quando
ela carrega. A regra global de `img` traz `height:auto` junto: sem isso, o
atributo `height` seria obedecido ao pé da letra e a logo do bloco "Sobre"
apareceria esticada.

**Efeito de brilho como assinatura visual.** A faixa de luz que atravessa os
elementos é feita só com CSS — `linear-gradient` inclinado e animado por
`keyframes`, sem imagem e sem JavaScript. É a referência ao polimento, que é
o serviço principal da casa.

**Animações respeitam `prefers-reduced-motion`.** Quem tem redução de
movimento ativada no sistema recebe a página estática.

## Tecnologias

`HTML5` · `CSS3` · `JavaScript` · `WebP` · `woff2` · `Netlify`

## Estrutura

```
index.html      pagina completa, com CSS e JS embutidos
fonts/          Poppins e Inter em .woff2, subset latin
img/            logo, foto principal, capa do video e favicons
video/          video de apresentacao
```

## Manutenção

A nota do Google (5.0) e o número de avaliações (30) estão escritos no
HTML, não vêm da API do Google — buscá-los ao vivo exigiria chave paga e uma
chamada a cada visita, o que não se justifica num site deste porte. Em
compensação, quando os números mudarem é preciso editá-los à mão. Eles
aparecem em quatro pontos do `index.html`, marcados com o comentário
`MANUTENCAO`.

Atenção especial à frase "100% com nota máxima": uma única avaliação abaixo
de cinco estrelas a torna falsa.

## Pendências

- [ ] Publicação no domínio oficial — trocar as URLs e remover o `noindex`
- [ ] Trocar a foto principal: a atual é um print de Instagram e traz os
      ícones da interface nos cantos de baixo

---

## Autor

**William dos Santos** — desenvolvedor web, Ubatuba/SP

[LinkedIn](https://www.linkedin.com/in/william-dos-santos-) ·
[Instagram](https://instagram.com/williamsantxs) ·
williamdsantos.souza@gmail.com
