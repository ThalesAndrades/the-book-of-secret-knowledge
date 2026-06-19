---
name: automated-review-response
description: >-
  Triagem e resposta a reviews automáticos de bots em PRs (CodeRabbit, Copilot,
  etc.) — distinguir banners "review in progress" de achados reais, aplicar
  nitpicks de lint Markdown com segurança e saber quando NÃO agir. Use ao
  monitorar/babysitar um PR ou processar eventos de webhook de review.
---

# Responding to Automated PR Reviews

Aprendido respondendo a um review do CodeRabbit em um PR.

## Triagem de comentários de bot — não reaja a tudo
- **Banners "review in progress" / ASCII art / poemas / "review stack"** →
  ruído, **nenhuma ação**. O CodeRabbit edita o mesmo comentário várias vezes;
  espere a versão final.
- **Walkthrough / pre-merge checks "✅ Passed"** → informativo. Se não há
  achados nem inline comments, o PR está verde — relate e siga.
- **"Rate limit reached" / "out of usage credits"** → informativo, sem ação.
  Pode-se reativar com `@coderabbitai review`, mas só se algo mudou de fato.
- **Nitpick / inline review comments com diff proposto** → **acionável**.

## Aplicando nitpicks de lint Markdown (comuns e seguros)
Correções de baixo risco que valem aplicar diretamente:
- **MD058** — exige linha em branco antes e depois de tabelas.
- **MD040** — blocos de código cercados precisam de identificador de linguagem
  (use ` ```text ` para listas de URLs/saída sem linguagem própria).
- **MD022/MD032** — linhas em branco ao redor de headings e listas.

Verifique cada achado contra o conteúdo atual, aplique o mínimo, e faça commit
com mensagem citando a regra (ex.: "Fix MD040: add language to code blocks").

## Quando perguntar antes de agir
- Achado **ambíguo** ou que toca algo arquiteturalmente significativo →
  use `AskUserQuestion`, não adivinhe.
- Sugestão que contraria uma decisão já tomada na conversa → confirme.

## Loop do webhook (Claude Code on web)
- Webhooks **não** entregam: sucesso de CI, novos pushes, merge/close,
  transição de conflito de merge. Não confie só em eventos.
- Não use `sleep` do Bash para esperar eventos externos.
- Não é possível chamar ferramentas MCP de dentro de um `Monitor` (bash puro);
  e `gh` pode não existir no ambiente. Para re-checar, prefira `send_later`
  quando disponível; caso contrário, peça ao usuário para avisar no merge.
- A inscrição só termina quando o PR é **merged** ou **closed**.
- Seja econômico: comente no PR apenas quando realmente necessário; o diff é o
  registro do que foi feito.
