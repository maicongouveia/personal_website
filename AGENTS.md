# AGENTS.md

Guia de orientação para agentes/harnesses de IA que forem trabalhar neste repositório.

## O que é este projeto

Site pessoal (portfólio/currículo) de Maicon Gouveia, publicado em `https://maicongouveia.com.br`.
Gerado com **Hugo** (static site generator, tema `dimension`), com conteúdo em **pt-br** (idioma
padrão) e **en**. Não é uma aplicação — não há backend, API, banco de dados ou testes automatizados.

## Estrutura do repositório

```
config.toml              # config do Hugo (idiomas, tema, título, baseURL)
content/                 # conteúdo-fonte do site (Markdown), fonte da verdade
  _index.{en,pt-br}.md       # página inicial
  sobre/_index.*.md          # página "Sobre" — ver "Página Sobre é single-page" abaixo
  sobre/formação/_index.*.md    # seção Formação (vira um modal/âncora dentro de /sobre/)
  sobre/profissional/_index.*.md # seção Carreira (idem)
  sobre/redes_sociais/_index.*.md # seção Contato (idem)
archetypes/default.md    # template usado por `hugo new`
themes/dimension/        # tema Hugo — submódulo git, ver "Build" abaixo
public/                  # OUTPUT gerado pelo Hugo — versionado no git e é o que
                          # é realmente publicado (ver seção Deploy)
.github/workflows/main.yml  # CI: publica public/ via FTP a cada push
.htaccess                # regras Apache (redirect www -> apex, https)
public/admin/            # Netlify CMS (decap) apontando para o git-gateway
```

Não existe `package.json`, nem test suite — não há `npm install`/`npm test` a rodar. Rodar `hugo`
exige o binário do Hugo instalado (ver "Build"); Go só é necessário se for compilar o próprio Hugo
a partir do fonte, não é uma dependência direta deste repositório.

## ⚠️ A página "Sobre" é single-page com modais — não são páginas separadas

O tema Dimension (HTML5 UP) é originalmente um site de página única com seções abertas via modal
por âncora. Isso se reflete direto no output do Hugo:

- O conteúdo de verdade, que os visitantes realmente veem, está todo dentro de **um único arquivo
  por idioma**: `public/sobre/index.html` (pt-br) e `public/en/sobre/index.html` (en). Cada
  subseção (`content/sobre/profissional/`, `sobre/formação/`, `sobre/redes_sociais/`) vira um
  `<article id="...">` dentro do mesmo `<div id="main">` dessa página, aberto via link de âncora no
  menu (`#carreira`, `#contato`, `#rm9ybwhdp8ojbw`/`#formação` etc.) — normalmente controlado por JS
  do tema (`assets/js/main.js`), não por navegação de página.
- O Hugo, por padrão, **também** gera uma página de listagem própria para cada seção (porque cada
  `_index.md` sem irmãos vira uma "list page" em `/sobre/profissional/`, `/sobre/formação/`,
  `/sobre/redes_sociais/`) — mas o layout de listagem do tema não renderiza `.Content`, então essas
  páginas saem **com o corpo vazio** (só título e subtítulo). **Isso é esperado, não é bug** — elas
  não são o que aparece no site para o usuário; ninguém navega para lá pelo menu. Não perca tempo
  tentando "consertar" essas páginas vazias — o alvo certo para qualquer edição de conteúdo dessas
  seções é sempre `public/sobre/index.html` / `public/en/sobre/index.html`.

## Fluxo de edição de conteúdo

O conteúdo-fonte fica em `content/**/*.md` (front matter YAML + corpo Markdown). Cada página tem
duas versões, uma por idioma, diferenciadas pelo sufixo do arquivo: `_index.pt-br.md` e
`_index.en.md`. **Ao editar um lado, verifique se o outro precisa do mesmo update** — eles já
estiveram dessincronizados no passado (ver "Inconsistências conhecidas de conteúdo" abaixo).

Depois de editar `content/`, é preciso rodar `hugo` para regenerar `public/` — ver "Build" abaixo.
Editar só `content/` sem regenerar `public/` não muda o site publicado, pois o deploy sobe
`public/` diretamente (não roda build em CI). Lembre que o conteúdo publicado relevante está
concentrado em `public/sobre/index.html` e `public/en/sobre/index.html` (ver seção acima) — ao
regenerar ou patchear manualmente, confirme que essas duas páginas ficaram corretas.

## Build

```
git submodule update --init --recursive   # busca themes/dimension (só necessário 1x por clone)
hugo                 # gera/atualiza public/ a partir de content/ + themes/dimension
hugo server -D       # servidor local com live reload, incluindo drafts
```

Requer o binário do Hugo instalado (testado com `hugo v0.166.0-extended`; no Windows,
`winget install --id Hugo.Hugo.Extended -e`).

`themes/dimension` é um **submódulo git de verdade** apontando para
`https://github.com/your-identity/hugo-theme-dimension.git`, registrado em `.gitmodules`. **Isso foi
corrigido recentemente** — até pouco tempo atrás, o gitlink existia no índice do git (modo `160000`,
commit `2474081b7846ce0e211c57b86ed84989548a777d`) mas sem `.gitmodules`, então
`git submodule update --init` não tinha URL para buscar e a pasta ficava vazia (build silenciosamente
não gerava nenhum HTML de página — `hugo` rodava sem erro fatal, só com avisos "no layout file for
kind home/section/taxonomy"). Se um checkout antigo/cache ainda tiver esse sintoma, rode
`git submodule update --init --recursive` (ou, se `themes/dimension` já existir vazio no working
tree e o comando reclamar, apague a pasta vazia antes e rode de novo).

Se por algum motivo o submódulo não puder ser buscado (offline, proxy, etc.): `public/` já contém o
HTML totalmente renderizado da build mais recente, então para alterações pequenas de texto é possível
editar `content/` e replicar a mudança manualmente em `public/**/index.html` (menos ideal, mas mantém
o site publicável). Prefira sempre rodar `hugo` de verdade quando possível — patch manual tem alto
risco de divergir do conteúdo-fonte (já aconteceu: ver commit que corrigiu a data de saída da Z1).

## Deploy

`.github/workflows/main.yml` roda em todo `push` e faz **apenas** um `FTP-Deploy-Action` que
sincroniza `./public/` para o servidor (`ftp.maicongouveia.com.br`) — **não há `hugo build` no
CI**. Consequências:
- O diretório `public/` precisa estar **atualizado e commitado** antes do push; se você editar
  `content/` sem rodar `hugo` e regenerar/commitar `public/`, o push publica conteúdo desatualizado.
- Não existe ambiente de staging/preview — todo push na branch configurada publica direto em
  produção.
- O secret `FTP_PASSWORD` vive nos GitHub Actions secrets do repositório (não neste checkout).

## Estado do repositório / branches

- `master` é a branch principal e é o que está checked out — reflete o site Hugo atual descrito
  acima.
- Existe uma branch remota `origin/rebrading-2025-10` que **apaga todo o conteúdo atual** (Hugo,
  tema, `content/`, `public/`) mantendo só `.htaccess` e o workflow — indício de um rebrand/reescrita
  do site em andamento que ainda não foi mergeado. **Não assuma que ela reflete o estado atual**;
  confirme com o usuário antes de basear qualquer trabalho nela.
- Outras branches remotas: `chore/remove-services-about-page`, `msg-release-20210502`.

## Inconsistências conhecidas de conteúdo (não são bugs de sistema, são de conteúdo)

- O corpo de texto de `content/sobre/profissional/_index.en.md` (exceto o que foi traduzido pontualmente,
  como a entrada da Omie) ainda está em português — nunca foi traduzido para inglês de fato, apenas o
  front matter (`title`, `description`) está em inglês. Isso é assim desde que o idioma `en` foi
  adicionado (commit `483eeca`). Se for pedida uma tradução completa da carreira, é trabalho novo, não
  uma correção de regressão.
- `content/sobre/redes_sociais/_index.en.md` tem um pequeno erro de digitação no front matter:
  `title: Contatc me` (deveria ser "Contact me") — esse typo também está em produção
  (`public/en/sobre/index.html`, `<article id="contatc-me">`).
- Existe uma pasta com nome acentuado `content/sobre/formação/` — cuidado com encoding ao manipular
  via shell (aparece como `forma\303\247\303\243o` em saídas não-UTF8 do git).
- `public/pt-br/**` é uma **árvore duplicada e obsoleta**, resultado de um `hugo server` (dev) que foi
  commitado por engano: os HTML lá dentro apontam assets para `http://localhost:1313/...` (CSS/imagens
  quebrados em produção) e incluem o script de livereload. O conteúdo também diverge do
  `public/sobre/index.html` "de verdade" em pelo menos um trecho (ex.: "Pix Direto" vs "Pix Indireto"
  na descrição da Z1). Apesar de obsoleta, essa árvore **está indexada** em `public/sitemap.xml`
  (`https://maicongouveia.com.br/pt-br/sitemap.xml`) e é servida publicamente. Isso é um problema
  pré-existente separado de qualquer edição de conteúdo — não tente corrigi-lo como patch pontual;
  ele exige rodar `hugo` de verdade (com `baseURL` de produção) e recommitar toda a árvore `public/`.
- O rodapé de todas as páginas atualmente publicadas está **sem a linha de atribuição do tema**
  (`© Design: d-asnaghi and HTML5 UP.`), que o layout do tema gera por padrão — um build limpo a
  traz de volta em todas as páginas. Não se sabe se isso foi removido de propósito (ex.: preferência
  de não exibir atribuição) ou é só resquício de builds antigas; **pergunte ao usuário antes de
  decidir** se ela deve voltar.

## Convenções de commit

Mensagens seguem o padrão `tipo: descrição` em português (`feat:`, `fix:`, `chore:`), estilo
Conventional Commits só que com o corpo em pt-br. Ex.: `feat: adicionando omie na area
profissional`, `fix: ci`.

## O que NÃO fazer sem confirmar com o usuário

- Não fazer push/deploy (todo push publica em produção via FTP, sem staging).
- Não migrar/mesclar a branch `rebrading-2025-10` para `master`.
- Não clonar/instalar dependências de repositórios de terceiros só com base em um palpite — o
  classificador de segurança do Claude Code bloqueia isso por padrão, e com razão. A URL do tema em
  `.gitmodules` foi confirmada pelo próprio usuário antes de ser usada.
- Não fazer um rebuild completo (`hugo` sobrescrevendo todo `public/`) sem avisar antes: o `public/`
  atual acumulou anos de artefatos legados (pasta `blog/`, `en/about/`, `pt-br/**` duplicado,
  diretórios `_index.*-copy` do CMS, `images/perfil.jpg`) que um build limpo remove — pode haver
  URLs indexadas/com backlink que dependam deles. Confirme com o usuário antes de fazer essa limpeza.
