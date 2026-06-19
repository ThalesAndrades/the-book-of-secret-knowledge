---
name: awesome-list-analysis
description: >-
  Produz um relatório de análise completo de uma awesome-list ou repositório
  centrado em README (estrutura, mapa de conteúdo por capítulo, estatísticas,
  saúde de links, pontos fortes/fracos e recomendações priorizadas). Use quando
  o pedido for genérico como "análise", "analise este repo", "relatório do
  repositório", ou ao auditar listas curadas grandes (awesome-*).
---

# Awesome-List / Repository Analysis

Como gerar um relatório de análise completo e fiel. Aprendido analisando
*The Book of Secret Knowledge* (README de 4.442 linhas, ~914 entradas).

## 0. Esclareça o escopo primeiro
Pedidos como "análise" são ambíguos. Use `AskUserQuestion` para escolher entre:
saúde de links · conteúdo/estrutura · qualidade/manutenção · **relatório
completo**. Não presuma — o entregável muda muito.

## 1. Reconhecimento da estrutura
```bash
wc -l README.md                                  # tamanho
grep -nE '^#### '  README.md                     # capítulos (ajuste o nível)
grep -cE '^##### ' README.md                     # nº de subseções
grep -oE '<a href=' README.md | wc -l            # entradas em <a href>
grep -oE '\]\([^)]+\)' README.md | wc -l         # links markdown
ls -R . ; ls -la .github                         # arquivos de governança
```

## 2. Mapa de conteúdo por capítulo (entradas por seção)
Detecte o padrão de headings primeiro; depois conte entradas `<a href>` por
capítulo com `awk`:
```bash
awk '
/^#### / { if(c!="") print n"\t"c; gsub(/&nbsp;.*/,""); gsub(/^#### /,""); c=$0; n=0; next }
/<a href=/ { n+=gsub(/<a href=/,"x") }
END { if(c!="") print n"\t"c }' README.md | sort -rn
```
Maiores subseções:
```bash
awk '/^##### /{if(s!=""&&c>0)print c"\t"s; sub(/.*: /,""); s=$0; c=0; next}
     /^#### /{if(s!=""&&c>0)print c"\t"s; s=""; c=0}
     /<a href=/{c+=gsub(/<a href=/,"x")}
     END{if(s!=""&&c>0)print c"\t"s}' README.md | sort -rn | head -15
```

## 3. Saúde de links
Use a skill **`link-health-check`** (extração dupla href+markdown, curl
paralelo com UA de navegador, e a armadilha dos parênteses). Reporte saúde
efetiva separando 404 reais de bloqueios anti-bot.

## 4. Estrutura do relatório (`ANALYSIS.md`)
Escreva no idioma do usuário. Seções que funcionaram bem:
1. **Visão Geral** — propósito, licença, tabela de métricas-chave, árvore de arquivos.
2. **Mapa de Conteúdo** — tabela de entradas por capítulo (com barras visuais) + maiores subseções.
3. **Saúde dos Links** — tabela de status com %, listas de quebrados reais, e nota sobre falsos positivos.
4. **Pontos Fortes** — concreto, baseado em evidências.
5. **Fragilidades e Riscos**.
6. **Recomendações Priorizadas** — tabela 🔴/🟡/🟢 com ação → benefício.
7. **Metodologia** — comandos usados + limitações (ex.: 403/000 podem ser anti-bot).

## Princípios
- **Seja fiel:** marque incertezas; distinga "morto" de "bloqueado".
- **Não invente números** (ex.: estrelas do GitHub) sem verificar.
- **Aditivo e não-destrutivo:** crie `ANALYSIS.md`, não altere o `README.md`
  sem ser pedido.
- **Verifique falsos positivos** antes de afirmar que algo está quebrado.
