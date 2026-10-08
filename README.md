# GEEKLESS

Jogo de adivinhar música no estilo *Songless*, com uma playlist de rap geek/anime brasileiro.

Toca um trecho curto da faixa — você tem 6 tentativas, e cada erro ou pulo libera mais alguns segundos. Quanto antes acertar, mais pontos.

### ▶ [Jogue aqui](https://crispedtoast836.github.io/GEEKLESS/)

Ou baixe o repositório e abra o `index.html` no navegador.

## Como funciona

| Tentativa | 1 | 2 | 3 | 4 | 5 | 6 |
|---|---|---|---|---|---|---|
| Segundos liberados | 1s | 2s | 4s | 6s | 9s | 13s |
| Pontos se acertar | 6 | 5 | 4 | 3 | 2 | 1 |

São 60 faixas; dá para jogar 5, 10 ou todas numa sessão. A ordem é sorteada a cada partida.

## Estrutura

```
index.html      o jogo inteiro (HTML, CSS e JS num arquivo só, sem dependências)
audio/          60 trechos de 15s, um .mp3 por faixa
```

Não tem build, framework nem servidor: é um site estático. A única coisa que vem de fora são as fontes do Google Fonts.

## Tecnologias

- **HTML, CSS e JavaScript puro**, sem frameworks
- **ffmpeg** para recortar os trechos e normalizar o volume dos áudios
- **GitHub Pages** para a hospedagem

## Trocar ou adicionar músicas

1. Recorte um trecho de ~15 segundos e normalize o volume (evita que uma faixa estoure e outra fique inaudível):

   ```bash
   ffmpeg -ss 60 -t 15 -i "musica-original.mp3" \
     -af loudnorm=I=-18:TP=-1.5:LRA=11 \
     -ac 2 -ar 44100 -b:a 112k audio/slug-da-musica.mp3
   ```

   O `-ss 60` é onde o trecho começa. Prefira o meio da música — o começo costuma ser instrumental e entrega menos.

2. Use um nome de arquivo sem acentos nem espaços (o `slug`).

3. Adicione a linha correspondente em `index.html`, no bloco `const TRACKS`:

   ```js
   {id:60, slug:"slug-da-musica", title:"Título da Música", artist:"Artista"},
   ```

O `title` é o que o jogador digita para acertar, e também o que aparece no autocomplete. O `id` só precisa ser único.

## Sobre os áudios

Os arquivos em `audio/` são trechos de 15 segundos usados para o jogo. Os direitos das músicas são dos respectivos artistas — este é um projeto pessoal, sem fins comerciais. Se for fazer a sua própria versão, use os seus próprios áudios.
