# Análise Completa do Repositório — *The Book of Secret Knowledge*

> Relatório gerado em **2026-06-19**. Baseado na inspeção do `README.md`
> (commit `7d37069`) e numa verificação automática de saúde de todos os
> links do documento.

---

## 1. Visão Geral

**The Book of Secret Knowledge** é uma *awesome-list* curada — uma coleção
de ferramentas, manuais, *cheat sheets*, one-liners e recursos voltados
principalmente para **administradores de sistemas e redes, DevOps, pentesters
e pesquisadores de segurança**.

Diferente da maioria das *awesome-lists* (que são apenas listas de links), este
repositório também embute **conhecimento prático executável**: centenas de
one-liners de shell, truques e funções comentados linha a linha.

| Característica | Valor |
|---|---|
| Licença | MIT (© 2017, trimstray) |
| Arquivo principal | `README.md` (~212 KB, **4.442 linhas**) |
| Capítulos | **15** |
| Subseções (`#####`) | **157** |
| Entradas de ferramentas/recursos (`<a href>`) | **914** |
| Links markdown adicionais | **78** |
| URLs únicas | **979** |
| Itens marcados como "temporariamente indisponível" (`*`) | 6 |

### Estrutura de arquivos
```
.
├── README.md                  # todo o conteúdo
├── LICENSE.md                 # MIT
├── static/img/                # imagem de preview
└── .github/
    ├── CONTRIBUTING.md
    ├── CODE_OF_CONDUCT.md
    └── FUNDING.yml
```

O repositório é deliberadamente minimalista: **todo o conteúdo vive em um único
`README.md`**, sem scripts, sem CI/CD, sem testes.

---

## 2. Mapa de Conteúdo (por capítulo)

Distribuição das **914 entradas** entre os 15 capítulos:

| # | Capítulo | Entradas | Peso |
|---|---|---:|---|
| 1 | Hacking/Penetration Testing | 203 | ████████████ |
| 2 | CLI Tools | 178 | ███████████ |
| 3 | Web Tools | 170 | ██████████ |
| 4 | Manuals/Howtos/Tutorials | 115 | ███████ |
| 5 | Blogs/Podcasts/Videos | 75 | █████ |
| 6 | Inspiring Lists | 58 | ███ |
| 7 | Systems/Services | 28 | ██ |
| 8 | Containers/Orchestration | 25 | ██ |
| 9 | GUI Tools | 24 | █ |
| 10 | Your daily knowledge and news | 16 | █ |
| 11 | Other Cheat Sheets | 13 | █ |
| 12 | Networks | 4 | ▏ |
| 13 | Shell One-liners | (conteúdo: ~2.685 linhas de código) | — |
| 14 | Shell Tricks | (conteúdo de código) | — |
| 15 | Shell Functions | (conteúdo de código) | — |

> Os três últimos capítulos não usam `<a href>`; são **blocos de código**
> (one-liners, truques e funções de shell) — representam cerca de **60% das
> linhas** do documento (≈ linhas 1661–4442).

### Maiores subseções
| Entradas | Subseção |
|---:|---|
| 56 | Pentesters arsenal tools |
| 55 | Pentests bookmarks collection |
| 46 | Labs (plataformas de ethical hacking / CTFs) |
| 40 | Mass scanners (search engines) |
| 37 | Network |
| 34 | Other |
| 27 | Security/Pentesting |

---

## 3. Saúde dos Links (verificação automática)

Todas as **979 URLs únicas** foram verificadas seguindo redirecionamentos,
com *user-agent* de navegador e timeout de 20 s.

| Status | Qtde | % | Interpretação |
|---|---:|---:|---|
| `200` OK | 835 | 85,3% | ✅ Saudáveis |
| `403 / 429` | 44 | 4,5% | ⚠️ Provável bloqueio anti-bot (Cloudflare) — provavelmente vivos no navegador |
| `503 / 5xx / 521 / 522` | 31 | 3,2% | ⚠️ Em sua maioria proteção anti-bot/CDN |
| `301` | 4 | 0,4% | ℹ️ Redirecionamento (atualizar para a URL final) |
| `404` Not Found | 37 | 3,8% | ❌ **22 reais** + 15 falsos positivos¹ |
| `000` falha de conexão/DNS | 28 | 2,9% | ❌ Domínios mortos / serviços descontinuados |

> ¹ **Falsos positivos:** 15 links da Wikipédia (ex.: `.../Dd_(Unix)`,
> `.../Find_(Unix)`, `.../Tar_(computing)`) contêm parênteses na URL e foram
> truncados pelo extrator. Reverificados individualmente, **todos retornam 200**
> e estão corretos no documento.

**Conclusão:** ~85% dos links estão claramente saudáveis. Considerando que a
maioria dos 403/429/503 são bloqueios automáticos (não quebras reais), a saúde
efetiva ultrapassa **90%** — excelente para uma lista deste tamanho e idade.

### 3.1 Links quebrados reais — `404` (candidatos a correção/remoção)
```
http://malc0de.com/database/
http://sandbox.onlinephpfunctions.com/
http://www.pc-help.org/obscure.htm
https://appsecco.com/books/subdomain-enumeration/
https://bitvijays.github.io/LFC-VulnerableMachines.html
https://github.com/GitHackTools/BillCipher
https://github.com/m4ll0k/Awesome-Hacking-Tools
https://github.com/payloadbox/command-injection-payload-list
https://github.com/rby90/Project-Based-Tutorials-in-C
https://github.com/sdcampbell/Internal-Pentest-Playbook
https://github.com/toolswatch/blackhat-arsenal-tools
https://github.com/twhite96/js-dev-reads
https://themanyhats.club/tag/episodes/
https://twitter.com/attcyber
https://viz.greynoise.io/table
https://wiki.skullsecurity.org/index.php?title=Passwords
https://www.amanhardikar.com/mindmaps/Practice.html
https://www.hackthis.co.uk/levels/
https://www.joedog.org/siege-home/
https://www.ostorlab.co/scan/mobile/
https://www.owasp.org/index.php/OWASP_Zed_Attack_Proxy_Project
https://www.trustedsec.com/category/articles/
```
> Nota: muitos repositórios GitHub `404` provavelmente foram renomeados ou
> tornados privados; vale buscar o novo endereço antes de remover. O link OWASP
> ZAP deve migrar para `https://www.zaproxy.org/`.

### 3.2 Falha de conexão / DNS — `000` (provavelmente descontinuados)
```
http://blog.safebuff.com/2016/07/03/SSRF-Tips/index.html
http://kb.entersoft.co.in/          http://mail2tor.com/
http://shell-storm.org/repo/CTF/    http://www.vclfiddle.net/
http://xip.io/                      https://1.1.1.1/
https://bgpview.io/                 https://brutelogic.com.br/blog/
https://chall.stypr.com             https://contained.af/
https://darksearch.io/              https://dnsprivacy.at/
https://engineering.videoblocks.com/web-architecture-101-...
https://hashes.org/                 https://inventory.rawsec.ml/index.html
https://lab.pentestit.ru/           https://labs.wizard-security.net/
https://packetlife.net/             https://pingme.io/
https://search.weleakinfo.com/      https://sploitus.com/
https://spyse.com/                  https://tools.intigriti.io/redirector/
https://weleakinfo.com              https://wiki.bash-hackers.org/start
https://www.hackergateway.com/      https://www.peerlyst.com/posts/...
```
> Vários destes são serviços **comprovadamente extintos** (ex.: `weleakinfo`
> foi apreendido pelo FBI; `spyse`, `peerlyst` e `darksearch` encerraram). Já
> `1.1.1.1`, `packetlife.net` e `bgpview.io` podem ser falsos positivos
> (bloqueiam clientes não-navegador). Recomenda-se verificação manual.

### 3.3 Redirecionamentos `301` (atualizar para a URL final)
```
http://dtrace.org/blogs/about/      https://dnstable.com/
https://findsubdomains.com/         https://www.ssllabs.com/ssltest/viewMyClient.html
```

---

## 4. Pontos Fortes

- **Curadoria de altíssima qualidade.** A política declarada — *"not meant to
  contain everything but only good quality stuff"* — é visível: as ferramentas
  listadas são padrões de mercado, não preenchimento.
- **Conteúdo executável**, não só links. Os one-liners/funções de shell são
  comentados linha a linha — funcionam como mini-tutoriais.
- **Organização consistente.** Padrão uniforme `#### Capítulo` →
  `##### :black_small_square: Subseção` → `<a href>Ferramenta</a> - descrição`,
  com links `[TOC]` de retorno em cada capítulo.
- **Governança presente:** `CONTRIBUTING.md`, `CODE_OF_CONDUCT.md`, `FUNDING.yml`
  e convenção explícita (`*`) para marcar links temporariamente fora do ar.
- **Saúde de links muito boa** (~85% `200` diretos) para um documento com quase
  mil URLs e ~9 anos de existência.

---

## 5. Fragilidades e Riscos

1. **Arquivo único e gigante.** 4.442 linhas / 212 KB em um só `README.md`
   tornam navegação, *diffs* e revisão de PRs difíceis. O GitHub trunca a
   pré-visualização de arquivos grandes.
2. **Sem verificação automática de links.** Não há CI; a degradação dos ~50
   links mortos passou despercebida. Um *link checker* agendado resolveria.
3. **Defasagem temporal.** As poucas referências datadas concentram-se em
   2017–2019; alguns serviços listados já encerraram.
4. **Acoplamento a domínios voláteis.** Listas de pentest dependem de serviços
   pequenos que somem (causa dos `000`).
5. **Sem índice das subseções.** O TOC cobre apenas os 15 capítulos; com 157
   subseções, um índice de segundo nível ajudaria.

---

## 6. Recomendações Priorizadas

| Prioridade | Ação | Benefício |
|---|---|---|
| 🔴 Alta | Adicionar **GitHub Action** de verificação de links (ex.: `lychee`/`markdown-link-check`) agendada (cron) | Detecta quebras automaticamente |
| 🔴 Alta | Corrigir/remover os **22 links `404` reais** e revisar os **28 `000`** (§3.1–3.2) | Restaura a confiança |
| 🟡 Média | Atualizar `OWASP ZAP` → `zaproxy.org` e os 4 redirecionamentos `301` | Links canônicos |
| 🟡 Média | Configurar o *link checker* para **ignorar parênteses** nas URLs da Wikipédia (evita falsos positivos) | Relatórios limpos |
| 🟢 Baixa | Considerar **dividir** o README por capítulo (`docs/`) mantendo um índice central | Manutenção/navegação |
| 🟢 Baixa | Adicionar **índice de subseções** (2º nível) | Descoberta de conteúdo |
| 🟢 Baixa | Marcar links instáveis confirmados com a convenção `*` existente | Coerência com as regras do projeto |

---

## 7. Metodologia

- **Inventário estrutural:** extração de headings (`####`/`#####`) e contagem de
  entradas `<a href>` por capítulo/subseção via `awk`/`grep`.
- **Saúde de links:** extração e *dedupe* de todas as URLs (`<a href>` +
  markdown), seguida de requisições `curl -L` (UA de navegador, timeout 20 s,
  24 em paralelo) sobre as **979 URLs únicas**.
- **Verificação de falsos positivos:** as URLs `404` com parênteses (Wikipédia)
  foram reverificadas individualmente com o parêntese de fechamento correto.

> ⚠️ Limitações: status `403/429/503/000` podem ser bloqueios anti-bot ou
> indisponibilidade momentânea, não necessariamente links permanentemente
> mortos. Recomenda-se confirmação manual antes de remover qualquer item — em
> linha com a regra do projeto: *"Please don't delete it without confirming
> that it has permanently expired."*
