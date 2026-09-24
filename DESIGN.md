---
name: Maicon Gouveia
description: Portfólio pessoal com a gramática de uma etiqueta de transportadora e um histórico de rastreamento.
colors:
  mailer-crimson: "#B01E28"
  mailer-deep: "#8C1720"
  on-mailer: "#FFF7F6"
  on-mailer-soft: "#F6CFD1"
  thermal-paper: "#F7F6F2"
  thermal-ink: "#141414"
  thermal-ink-soft: "#4A4743"
typography:
  display:
    fontFamily: "Barlow Condensed, Arial Narrow, sans-serif"
    fontSize: "clamp(2.6rem, 7.4vw, 6rem)"
    fontWeight: 800
    lineHeight: 0.86
    letterSpacing: "-0.005em"
  headline:
    fontFamily: "Barlow Condensed, Arial Narrow, sans-serif"
    fontSize: "clamp(2.2rem, 5vw, 3.6rem)"
    fontWeight: 800
    lineHeight: 0.95
  title:
    fontFamily: "Barlow Condensed, Arial Narrow, sans-serif"
    fontSize: "clamp(2rem, 3.6vw, 2.6rem)"
    fontWeight: 800
    lineHeight: 0.95
  body:
    fontFamily: "Barlow, Segoe UI, system-ui, sans-serif"
    fontSize: "1.0625rem"
    fontWeight: 400
    lineHeight: 1.6
  label:
    fontFamily: "Azeret Mono, ui-monospace, monospace"
    fontSize: "0.6875rem"
    fontWeight: 500
    letterSpacing: "0.1em"
rounded:
  stamp: "3px"
  label: "4px"
spacing:
  gutter: "clamp(16px, 4vw, 40px)"
  row: "18px 24px"
  event: "34px"
components:
  button-solid:
    backgroundColor: "{colors.thermal-ink}"
    textColor: "{colors.thermal-paper}"
    rounded: "{rounded.label}"
    padding: "10px 18px"
    height: "48px"
  button-solid-hover:
    backgroundColor: "{colors.mailer-crimson}"
    textColor: "{colors.thermal-paper}"
  button-line:
    backgroundColor: "{colors.thermal-paper}"
    textColor: "{colors.thermal-ink}"
    rounded: "{rounded.label}"
    padding: "10px 18px"
    height: "48px"
  button-line-hover:
    backgroundColor: "{colors.thermal-ink}"
    textColor: "{colors.thermal-paper}"
  status-chip:
    backgroundColor: "{colors.mailer-crimson}"
    textColor: "{colors.thermal-paper}"
    typography: "{typography.label}"
    padding: "3px 7px 2px"
  label:
    backgroundColor: "{colors.thermal-paper}"
    textColor: "{colors.thermal-ink}"
    rounded: "{rounded.label}"
    padding: "14px"
---

# Design System: Maicon Gouveia

## Overview

**Creative North Star: "A Remessa Rastreada"**

O site é uma encomenda em trânsito. O fundo é o envelope plástico carmesim de uma transportadora,
e todo conteúdo vive em etiquetas de papel térmico coladas sobre ele: uma etiqueta grande de
destinatário no topo, uma folha contínua de histórico de rastreamento e volumes anexos menores. A
metáfora é só gramática visual; o texto continua factual e em primeira pessoa.

A densidade é de documento logístico: campos com filete preto, cada campo guardando um único fato,
datas e códigos em mono de impressora térmica, nomes em grotesca condensada pesada. A tinta é
chapada e a impressão é seca: nada desliza, as coisas aparecem em cortes.

**Key Characteristics:**
- Envelope carmesim cobre toda a página (estratégia Committed); o conteúdo longo mora no papel.
- Etiquetas com moldura impressa interna de 2px e cantos de corte de faca (4px).
- Grotesca condensada em caixa-alta para nomes; mono para dados; Barlow para leitura.
- Código de barras Code 128 real como link de e-mail.
- Movimento em `steps()`, sem easing.

## Colors

Duas superfícies e uma tinta: o plástico carmesim e o papel térmico, com preto de impressão.

### Primary
- **Carmesim de Envelope** (mailer-crimson): o fundo da página inteira e a cor de marca mantida do
  site anterior. Sobre o papel, marca o que está vivo: status "Em rota", o time atual, o ponto do
  evento atual, carimbos e hover dos botões.
- **Carmesim Profundo** (mailer-deep): barra de navegação fixa.

### Neutral
- **Papel Térmico** (thermal-paper): fundo de toda etiqueta, folha e volume.
- **Tinta Térmica** (thermal-ink): texto, filetes, trilho do rastreio, caixa de triagem "MG".
- **Tinta Desbotada** (thermal-ink-soft): rótulos de campo, stack, numeração de sequência.
- **Branco de Envelope** (on-mailer) e **Rosa de Envelope** (on-mailer-soft): texto sobre o
  carmesim; o rosa é o secundário (contraste 4.8:1 sobre o carmesim).

### Named Rules
**The Two Surfaces Rule.** Só existem o envelope e o papel. Nenhum terceiro fundo, nenhum cinza de
cartão, nenhum gradiente.

**The Live Ink Rule.** Sobre o papel, o carmesim marca apenas o que é atual ou acionável. Texto
secundário nunca é carmesim.

## Typography

**Display Font:** Barlow Condensed (com Arial Narrow)
**Body Font:** Barlow (com Segoe UI, system-ui)
**Label/Mono Font:** Azeret Mono (com ui-monospace)

**Character:** A condensada tem o registro de etiqueta de despacho e placa rodoviária; a Azeret
Mono é a cabeça da impressora térmica. As duas só aparecem onde o objeto real as teria.

### Hierarchy
- **Display** (800, clamp 2.6–6rem, 0.86): o nome na etiqueta de destinatário e o "Vamos
  conversar?" do fechamento.
- **Headline** (800, clamp 2.2–3.6rem, 0.95): títulos de seção, sempre em caixa-alta.
- **Title** (800, clamp 2–2.6rem, 0.95): nome de cada empresa no histórico e de cada volume.
- **Body** (400, 1.0625rem, 1.6): descrições, com no máximo 68ch.
- **Label** (Azeret Mono 500, 0.6875rem, tracking 0.1em, caixa-alta): rótulos de campo, datas,
  códigos e carimbos.

### Named Rules
**The Field Label Rule.** Rótulo mono fica ao lado ou dentro do campo que descreve, nunca como
kicker acima de um título de seção. "Destinatário" corre na vertical, à esquerda do nome.

**The Mono Is Data Rule.** Mono só para datas, códigos, stack e rótulos de campo; nunca para prosa.

## Layout

Coluna central de até 1200px com gutter fluido (16–40px). O primeiro viewport é uma grade de
1.6fr/1fr: a etiqueta à esquerda, girada −0.8°, e "Últimos eventos" à direita, alinhado ao topo,
sobre o carmesim. O histórico é uma folha larga de papel, e cada evento é uma grade de quatro
colunas: sequência (2.4rem), trilho (18px), data (12.5rem) e corpo. Formação e projetos ficam lado a
lado (1fr/1.35fr). Acima de 960px, a coluna mais curta de cada par ("Últimos eventos" e
"Formação") fica fixa a 88px do topo e acompanha a rolagem ao lado da coluna longa, em vez de
deixar um vão.

Abaixo de 960px tudo vira uma coluna e a rotação sai. Abaixo de 720px as âncoras da nav somem (fica
só "MG" e o idioma), os campos da etiqueta viram uma grade 2×2, a sequência numérica some, a data
sobe para cima do nome e a folha de histórico ocupa a largura total, sem cantos.

**The Heading Air Rule.** Seções ganham 72–128px acima e 24px entre título e conteúdo.

## Elevation & Depth

Profundidade física e mínima: o papel está colado no plástico. Existe uma só sombra, de contato,
curta e sem halo.

### Shadow Vocabulary
- **Contato** (`box-shadow: 0 1px 0 rgba(60,0,8,.28), 0 3px 4px -2px rgba(40,0,6,.35)`): toda
  etiqueta, folha e volume.

**The Glued Paper Rule.** Nada flutua. Sombra difusa grande, glow ou sombra dura deslocada estão
fora do mundo.

## Shapes

Retângulos de etiqueta com cantos de corte de faca (4px na etiqueta e na folha, 3px nos volumes),
uma moldura impressa interna de 2px a 14px da borda e linhas internas separadas por filetes pretos
de 2px. O canhoto da stack é separado por um picote tracejado. Os pontos do rastreio são os únicos
círculos. Carimbos são retângulos de 1.5px levemente girados (−1.5°).

## Components

### Buttons
- **Shape:** corte de etiqueta (4px), altura mínima de 48px, Barlow Condensed 700 em caixa-alta.
- **Solid:** tinta chapada com texto em papel; no hover vira carmesim, com troca seca.
- **Line:** filete de 2px de tinta; no hover inverte para tinta chapada.
- **Focus:** outline de 3px na cor da tinta sobre o papel e na cor do texto sobre o carmesim.

### Etiqueta (signature)
Papel térmico com moldura impressa e linhas: cabeçalho (caixa de triagem "MG" invertida + serviço
+ código de rastreio), destinatário (nome em Display, rótulo vertical), grade de campos com um fato
cada, faixa do código de barras com as ações e o canhoto "Conteúdo declarado" com a stack inteira.

### Histórico de rastreamento (signature)
Trilho vertical contínuo de 2px com um ponto por empresa: preenchido em tinta para eventos passados,
carmesim com halo para o atual (com o carimbo "Em rota"). Eventos separados por um filete tracejado.
A stack de cada evento fica em mono, separada por barras.

### Carimbos e chips
- **Status:** carmesim chapado com texto em papel, em Label mono.
- **Carimbo de volume:** contorno carmesim de 1.5px, texto carmesim, girado −1.5°.

### Navigation
Barra fixa em carmesim profundo, com 60px. Monograma "MG" em caixa com contorno (inverte no
hover), âncoras em condensada caixa-alta rosa de envelope (brancas e sublinhadas no hover) e troca
de idioma em mono com contorno.

### Código de barras
Code 128B real do e-mail, desenhado como um único path SVG que estica na largura (`preserveAspectRatio="none"`), com a
legenda em mono abaixo. É sempre um link `mailto:`. No hover a tinta vira carmesim.

## Do's and Don'ts

### Do:
- **Do** colocar todo conteúdo novo numa etiqueta de papel sobre o envelope, com a moldura
  impressa de 2px.
- **Do** dar um único fato a cada campo e uma ordem fixa de leitura.
- **Do** animar só em `steps()` (impressão por faixa, carimbo), sempre dentro de
  `prefers-reduced-motion: no-preference`.
- **Do** manter pt-br e en idênticos em estrutura.

### Don't:
- **Don't** usar sombra difusa grande, cantos acima de 4px, gradientes ou glass.
- **Don't** colocar kicker/eyebrow acima de títulos de seção; rótulos mono pertencem a campos.
- **Don't** usar mono em prosa, nem carmesim em texto secundário sobre o papel.
- **Don't** transformar a metáfora em piada no texto: a copy continua factual.
