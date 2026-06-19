---
name: link-health-check
description: >-
  Verifica a saúde de todos os links de um arquivo Markdown/README (ou de um
  repositório inteiro) — detecta links quebrados (404), domínios mortos
  (falha de conexão/DNS) e redirecionamentos. Use quando o pedido envolver
  "checar links", "links quebrados", "dead links", "link rot", "validar URLs"
  ou auditar um README cheio de referências externas.
---

# Link Health Check

Auditoria automática de links em Markdown/HTML. Aprendido auditando o README
de uma *awesome-list* com ~980 URLs únicas.

## Procedimento

### 1. Extrair e deduplicar TODAS as URLs
Os links aparecem em dois formatos — capture os dois:

```bash
# <a href="https://..."> (HTML embutido, comum em awesome-lists)
grep -oE 'href="https?://[^"]+"' README.md | sed -E 's/href="//; s/"$//' > /tmp/urls_href.txt
# [texto](https://...) (markdown puro)
grep -oE '\]\(https?://[^) ]+\)' README.md | sed -E 's/^\]\(//; s/\)$//' > /tmp/urls_md.txt
cat /tmp/urls_href.txt /tmp/urls_md.txt | sort -u > /tmp/urls_all.txt
wc -l /tmp/urls_all.txt
```

### 2. Checar em paralelo, com user-agent de navegador
UA de navegador é **essencial** — muitos sites devolvem 403/503 para clientes
"robôs". Siga redirecionamentos (`-L`) e use timeout.

```bash
check_url() {
  code=$(curl -sS -L --max-time 20 -o /dev/null -w "%{http_code}" \
    -A "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120 Safari/537.36" \
    "$1" 2>/dev/null)
  printf "%s\t%s\n" "${code:-000}" "$1"
}
export -f check_url
cat /tmp/urls_all.txt | xargs -P 24 -I {} bash -c 'check_url "$@"' _ {} > /tmp/url_results.txt
awk -F'\t' '{print $1}' /tmp/url_results.txt | sort | uniq -c | sort -rn   # distribuição
```

### 3. Interpretar os status (NÃO trate tudo como quebrado)

| Status | Significado | Ação |
|---|---|---|
| `200` / `3xx` final 200 | Saudável | OK |
| `403`, `429`, `503`, `521/522` | Quase sempre **bloqueio anti-bot/CDN** (Cloudflare), não link morto | NÃO remover; verificar no navegador |
| `404` | Página não existe | Candidato real a correção/remoção |
| `000` | Falha de DNS/conexão/timeout | Domínio provavelmente extinto — mas confirmar (alguns bloqueiam curl) |
| `301` (final) | Redireciona | Atualizar para a URL canônica |

```bash
awk -F'\t' '$1=="404"{print $2}' /tmp/url_results.txt | sort   # 404s
awk -F'\t' '$1=="000"{print $2}' /tmp/url_results.txt | sort   # falhas de conexão
awk -F'\t' '$1 ~ /^3/{print $1" "$2}' /tmp/url_results.txt      # redirects
```

## ⚠️ Armadilha crítica: parênteses na URL (falsos positivos)

URLs com parênteses (clássico: Wikipédia `.../Dd_(Unix)`, `.../Tar_(computing)`)
em links markdown `[x](url)` são **truncados** pelo regex no primeiro `)`,
gerando 404 falsos. **Sempre reverifique os 404 que contêm `(` re-adicionando
o `)` de fechamento** antes de reportá-los como quebrados:

```bash
curl -sS -L --max-time 20 -o /dev/null -w "%{http_code}\n" -A "Mozilla/5.0" \
  "https://en.wikipedia.org/wiki/Dd_(Unix)"   # -> 200, link está OK
```

## Regras de relato
- Reporte saúde efetiva separando "quebrados reais" de "bloqueios anti-bot".
- Antes de sugerir remoção, lembre da convenção comum em awesome-lists: não
  apagar um link sem confirmar que expirou **permanentemente**.
- Para automatizar de forma recorrente, recomende uma GitHub Action com
  `lychee` ou `markdown-link-check` (configurada para ignorar parênteses).
