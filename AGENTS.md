# AGENTS.md

Guia de orientação para agentes/harnesses de IA que forem trabalhar neste repositório.

## O que é este projeto

Site pessoal (portfólio/currículo) de Maicon Gouveia, publicado em `https://maicongouveia.com.br`.
É um site **estático, escrito à mão** (HTML/CSS puro, sem build step, sem framework, sem
dependências de Node/npm) — não é uma aplicação, não há backend, API, banco de dados ou testes
automatizados.

O site já usou o gerador estático **Hugo** (tema `dimension`) até setembro/2026. Essa estrutura foi
removida por completo — não existe mais `content/`, `config.toml`, `archetypes/`, `themes/` nem
submódulos git. Se você encontrar referências a isso em commits antigos ou em memória de uma
conversa anterior, está desatualizado: **o que está em `public/` hoje é a fonte da verdade, editada
diretamente.**

## Estrutura do repositório

```
public/                     # TUDO que é publicado — é a fonte da verdade, editada diretamente
  index.html                    # home em pt-br (idioma padrão)
  en/index.html                 # home em en
  css/site.css                  # CSS único usado pelas duas páginas acima
  watchmycar/                   # site arquivado do TCC "WatchMyCar" (republicado em /watchmycar/)
  .htaccess                     # regras Apache (redirect www -> apex, https) — cópia da raiz
docs/                        # documentação de referência (não lida por nenhum processo de build)
  conteudo.pt-br.md             # resumo do conteúdo textual da home em pt-br
  content.en.md                 # resumo do conteúdo textual da home em en
.htaccess                    # mesma regra de redirect, na raiz (não é publicada; o que vale é
                              # public/.htaccess, que o deploy sobe)
.github/workflows/main.yml   # CI: publica public/ via FTP a cada push
AGENTS.md / CLAUDE.md        # este guia
```

Não existe `package.json` nem test suite — não há `npm install`/`npm test`/build algum a rodar.
Editar o site é editar HTML/CSS diretamente em `public/`.

## Fluxo de edição de conteúdo

Não há passo de build. Para mudar qualquer coisa visível no site, edite diretamente:
- `public/index.html` — home em português (idioma padrão, servida em `/`)
- `public/en/index.html` — home em inglês (servida em `/en/`)
- `public/css/site.css` — estilos compartilhados pelas duas páginas acima

As duas páginas têm a mesma estrutura de seções (`#formacao`/`#education`, `#experiencia`/
`#experience`, `#projetos`/`#projects`, `#contato`/`#contact`), só o texto muda. **Ao editar uma,
verifique se a outra precisa do mesmo update** — é fácil elas ficarem dessincronizadas.

`docs/conteudo.pt-br.md` e `docs/content.en.md` guardam um resumo em prosa do que está nas duas
páginas (histórico profissional completo, formação, projetos, contato) — útil como referência
rápida sem precisar reler o HTML inteiro, mas **não é a fonte de verdade e nenhum processo os lê**;
se o conteúdo do site mudar, edite o HTML e, se ainda fizer sentido, atualize esses arquivos também
(eles podem ficar defasados sem que isso quebre nada).

`public/watchmycar/` é o site arquivado de um projeto antigo (TCC), publicado como está, sem
edição — não faz parte do conteúdo "vivo" do portfólio.

## Deploy

`.github/workflows/main.yml` roda em todo `push` e faz **apenas** um `FTP-Deploy-Action` que
sincroniza `./public/` para o servidor (`ftp.maicongouveia.com.br`). Esse sync é um espelhamento:
**arquivos removidos de `public/` localmente somem do servidor no próximo push.** Consequências:
- Não existe ambiente de staging/preview — todo push na branch configurada publica direto em
  produção.
- Qualquer arquivo em `public/` é publicado como está — não há transformação nenhuma.
- O secret `FTP_PASSWORD` vive nos GitHub Actions secrets do repositório (não neste checkout).

## Estado do repositório / branches

- `master` é a branch principal e é o que está checked out — reflete o site estático atual descrito
  acima.
- Existe uma branch remota `origin/rebrading-2025-10` que **apaga todo o conteúdo atual** mantendo
  só `.htaccess` e o workflow — indício de um rebrand/reescrita do site que ainda não foi mergeado.
  **Não assuma que ela reflete o estado atual**; confirme com o usuário antes de basear qualquer
  trabalho nela.
- Outras branches remotas: `chore/remove-services-about-page`, `msg-release-20210502`.

## Inconsistências conhecidas de conteúdo (não são bugs de sistema, são de conteúdo)

- `content/sobre/redes_sociais` chegou a ter o typo "Contatc me" no front matter em inglês (era do
  Hugo). Já foi corrigido no `public/en/index.html` atual — não deve reaparecer, mas fica registrado
  aqui caso apareça de novo em algum patch manual.

## Convenções de commit

Mensagens seguem o padrão `tipo: descrição` em português (`feat:`, `fix:`, `chore:`), estilo
Conventional Commits só que com o corpo em pt-br. Ex.: `feat: adicionando omie na area
profissional`, `fix: ci`.

## O que NÃO fazer sem confirmar com o usuário

- Não fazer push/deploy (todo push publica em produção via FTP, sem staging).
- Não migrar/mesclar a branch `rebrading-2025-10` para `master`.
- Não remover/reescrever URLs publicadas em `public/` (ex.: `/watchmycar/`) sem avisar antes — podem
  existir backlinks ou indexação do Google apontando pra lá.
- Não reintroduzir um gerador estático (Hugo ou outro) sem alinhar com o usuário — a decisão de ir
  para HTML/CSS estático puro foi deliberada.
