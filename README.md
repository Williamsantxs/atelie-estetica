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

**Efeito de brilho como assinatura visual.** A faixa de luz que atravessa os
elementos é feita só com CSS — `linear-gradient` inclinado e animado por
`keyframes`, sem imagem e sem JavaScript. É a referência ao polimento, que é
o serviço principal da casa.

**Animações respeitam `prefers-reduced-motion`.** Quem tem redução de
movimento ativada no sistema recebe a página estática.

## Tecnologias

`HTML5` · `CSS3` · `JavaScript` · `WebP` · `Netlify`

## Estrutura

```
index.html      pagina completa, com CSS e JS embutidos
img/            logo, foto principal e capa do video
video/          video de apresentacao
```

## Pendências

- [ ] Publicação no domínio oficial — trocar as URLs e remover o `noindex`
- [ ] Converter a logo para WebP e reduzir para o tamanho de exibição

---

## Autor

**William dos Santos** — desenvolvedor web, Ubatuba/SP

[LinkedIn](https://www.linkedin.com/in/william-dos-santos-) ·
[Instagram](https://instagram.com/williamsantxs) ·
williamdsantos.souza@gmail.com
