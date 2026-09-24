---
version: 1
slug: "public-index-html"
primary_target: "public/index.html"
related_targets: ["public/en/index.html"]
---

# Home (pt-br `/` e en `/en/`)

Escopo: as duas homes espelhadas, com CSS compartilhado. Modo: Persuade. O visitante (público misto:
recrutador, cliente, par) entende em segundos quem é Maicon, onde trabalhou e desde quando, e então
entra em contato ou abre LinkedIn/GitHub/projetos. Prova: histórico real, 700 mil cadastros (Z1),
imprensa do WatchMyCar e o RPG com 26 sessões. Restrições: HTML/CSS puro, carmesim e monograma MG
mantidos, paridade pt/en, analytics sem cookies (GoatCounter) nos cliques de contato/perfis/projetos.

## Direction contract

THESIS: A carreira como remessa rastreada. Etiqueta térmica de transportadora mais o histórico de
rastreamento; cada empresa é um evento datado. Recusa o portfólio de dev em coluna única com
tags coloridas e o hero escuro de terminal.

OWN-WORLD: fundo de envelope plástico carmesim (#A3121E a #B01E28, em estratégia Committed) com
etiquetas em papel térmico quase branco (#F7F5EF) e tinta térmica preta (#111). Campos delimitados
por filetes pretos de 2px, rótulos de campo em caixa-alta miúda, grotesca condensada pesada (Barlow
Condensed) para nomes, mono de impressora térmica (Azeret Mono) para datas e códigos, código de
barras Code 128 real, caixa de triagem "MG" invertida. Sem sombras suaves, sem cantos arredondados
grandes, sem gradientes.

STORY: vê a etiqueta com nome, função e 8+ anos; varre os campos numa ordem fixa; desce pelo
histórico 06→01 com a coluna numerada; encontra a stack inteira no bloco de letras miúdas; lê
formação e projetos como volumes anexos; o código de barras final leva ao e-mail.

FIRST VIEWPORT: faixa de nav fina sobre o carmesim (MG, âncoras, EN). À esquerda, cerca de 60% da
largura: a etiqueta levemente girada (-0.8deg, 0 no mobile) com o bloco DESTINATÁRIO, MAICON
GOUVEIA em 88–120px condensado, a função, o pitch, a grade de campos (DESDE 2017 · EMPRESAS 6 · STATUS
EM ROTA · OMIE) e o código de barras de e-mail com o CTA "Entrar em contato". À direita, em
tinta branca sobre o carmesim: "ÚLTIMOS EVENTOS", os 3 eventos mais recentes com linha e pontos de
rastreamento, e o link "Ver histórico completo".

FORM: etiqueta de transportadora e rastreamento de encomenda; 4º da lista ordenada; seed 75ff0043.
Assinatura: a etiqueta "imprime" linha a linha ao carregar, com cortes secos e sem ease (herança
das válvulas nixie). Os eventos do rastreio se acendem em passos ao entrar na tela. Tudo desligado
com prefers-reduced-motion.

FINISH: unreviewed and undocumented is unfinished; this build ends with the finish review, the verdict, DESIGN.md, and every shipping raster carrying its provenance
