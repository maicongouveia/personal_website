# Product

<!-- impeccable:product-schema 1 -->

## Platform

web

## Users
Público misto, sem prioridade declarada: recrutadores e tech leads avaliando para vagas, possíveis
clientes de projetos, e pares/comunidade. O site precisa funcionar para uma leitura rápida
(senioridade, empresas, stack) e para quem quer se aprofundar (projetos, histórico completo).

## Product Purpose
Site pessoal/portfólio de Maicon Gouveia (maicongouveia.com.br): apresenta trajetória profissional,
formação, projetos e canais de contato, em pt-br (padrão, `/`) e en (`/en/`).

Métrica de sucesso: **em aberto.** O usuário ainda não definiu qual ação conta como sucesso
(contato, clique em LinkedIn/GitHub, visita a projetos) e quer passar a medir isso. Hoje não há
nenhum analytics no site. Decidido: incluir analytics sem cookies (sem banner de consentimento,
compatível com LGPD) contando visitas e cliques em e-mail, LinkedIn, GitHub e projetos, para
depois definir a métrica de sucesso com dados.

## Positioning
Desenvolvedor de software generalista sênior: 8+ anos em produtos de missão crítica
(marketplaces, logística, fintechs), do planejamento à manutenção em produção, com amplitude de
stacks e empresas (Omie, Z1, Mercado Livre, Loggi, MadeinWeb). Integrações com sistemas externos
(bancos, Pix/Bacen, Mercado Pago, clientes da Loggi) aparecem em quase toda a trajetória, mas o
posicionamento escolhido é a amplitude, não um nicho.

## Capabilities and Constraints
- HTML/CSS estático escrito à mão em `public/`, sem build step nem framework (decisão deliberada;
  não reintroduzir gerador estático sem alinhar).
- Duas páginas espelhadas: `public/index.html` (pt-br) e `public/en/index.html` (en), com o CSS
  compartilhado `public/css/site.css`. Toda mudança vale para as duas.
- Deploy: push → FTP para produção, sem staging.
- `/watchmycar/` é um site arquivado que deve continuar publicado como está.
- Seções âncora existentes: `#formacao`/`#education`, `#experiencia`/`#experience`,
  `#projetos`/`#projects`, `#contato`/`#contact`.

## Brand Commitments
- Nome: Maicon Gouveia. Favicon atual: monograma "MG" (`public/favicon.svg`).
- Voz: primeira pessoa, direta, factual.
- Mantidos no redesign (escolha do usuário): o acento carmesim (hoje `#B01E28`) como cor de marca
  e o monograma "MG". O modo escuro automático não é compromisso; o resto do visual antigo pode
  ser substituído.
- O resultado não pode parecer template de portfólio, nem frio/corporativo sem personalidade, nem
  difícil de escanear (empresas, datas e stack precisam ser achados em segundos).

## Evidence on Hand
- Histórico profissional completo com períodos, times, responsabilidades e tecnologias
  (`docs/conteudo.pt-br.md`, `docs/content.en.md`).
- Número concreto: 700 mil cadastros no onboarding da Z1.
- Imprensa do TCC WatchMyCar: Globo Auto Esporte (31/01/2016), Exame Arena Tech (11/03/2016).
- Projeto pessoal "Odisseia dos Lordes Dragões": pipeline em Python com LLM e geração de imagem,
  publicado em rpg.maicongouveia.com.br.
- Não existem foto profissional, depoimentos, métricas de tráfego nem estudos de caso. Não
  inventar nada disso.

## Product Principles
1. Leitura rápida primeiro: senioridade, empresas e stack visíveis em segundos para quem só dá uma
   olhada.
2. Profundidade disponível: quem quiser detalhes encontra o histórico completo sem sair da página.
3. Só fatos verificáveis: nada de números, depoimentos ou alegações que não estejam no histórico.
4. Paridade pt-br/en: as duas versões sempre têm o mesmo conteúdo.
5. Leve e sem dependências: HTML/CSS puro que carrega rápido e dura sem manutenção.
