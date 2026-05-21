---
name: agent-social-maneger
description: "Gerenciamento autonomo e assistido de redes sociais, conteudo, comunidade, direct messages, metricas e midia paga para o agente Zeus. Use quando o usuario pedir para conectar Instagram, TikTok, YouTube, Facebook, LinkedIn, X/Twitter, Threads ou outras redes; criar posts, reels, shorts, carrosseis, roteiros, thumbnails ou imagens; responder comentarios e DMs; analisar metricas; planejar, subir, pausar, otimizar ou relatar campanhas de Meta Ads, Google Ads, YouTube Ads ou TikTok Ads."
---

# Agent Social Maneger

## Objetivo

Atuar como skill operacional do Zeus para gerenciar presenca social, conteudo, comunidade e Ads em contas conectadas ao OpenCloud/OpenClaw. Use APIs oficiais, conectores autorizados, OAuth, webhooks e ferramentas disponiveis no ambiente; se a integracao ao vivo nao existir, entregue plano tecnico, rascunhos, payloads ou codigo de integracao sem fingir execucao.

## Modo Padrao

Comece em **Modo Assistido** salvo configuracao explicita em contrario.

- **Rascunho**: criar conteudos, respostas, calendarios, relatorios e campanhas sem publicar ou gastar.
- **Assistido**: executar publicacoes e respostas simples quando permitido, mas pedir aprovacao para Ads, DMs proativas, temas sensiveis e mudancas de conta.
- **Autonomo Controlado**: executar dentro de limites pre-aprovados de conta, plataforma, orcamento, publico, tom de voz e tipos de acao.

Nao trate "permissao uma vez" como permissao ilimitada. Converta a permissao em um manifesto de limites e respeite-o em todas as acoes.

## Roteamento De Referencias

Leia somente o arquivo necessario para a tarefa:

- Rodar o wizard completo de conexao, permissao, teste e ativacao: `references/connection-wizard.md`.
- Escolher formas simples de autenticacao antes de implementar OAuth completo: `references/simple-auth.md`.
- Conectar contas, validar tokens, mapear APIs ou webhooks: `references/integrations.md`.
- Criar posts, carrosseis, scripts, imagens, thumbnails, calendarios ou publicacoes: `references/content-production.md`.
- Responder comentarios, moderar comunidade ou operar directs: `references/community-management.md`.
- Criar, subir, pausar, escalar ou otimizar Ads: `references/ads-management.md`.
- Analisar metricas, criar dashboards ou relatorios: `references/metrics-reporting.md`.
- Definir autonomia, aprovacoes, logs, privacidade e limites: `references/autonomy-safety.md`.

## Preflight Obrigatorio

Antes de qualquer acao ao vivo:

1. Identifique plataforma, conta, objetivo, modo de autonomia e ferramenta disponivel.
2. Confirme que a credencial existe em storage seguro, variavel de ambiente, conector ou secret manager. Nunca solicite senha em texto puro.
3. Verifique se a acao cabe no manifesto de permissao: contas, orcamento, regioes, publicos, tipos de conteudo, DMs e temas permitidos.
4. Valide politicas da plataforma e leis aplicaveis para a categoria do conteudo.
5. Gere rascunho/payload e faca checagem de qualidade antes de publicar, responder ou gastar.
6. Registre a acao no log operacional com data, plataforma, conta, objetivo, payload resumido, gasto previsto e resultado.

Se qualquer item falhar, opere em modo rascunho e explique o bloqueio.

## Regras Inviolaveis

- Use somente APIs oficiais, conectores permitidos e automacoes aceitas pelas plataformas.
- Nao compre seguidores, curtidas, comentarios, visualizacoes ou qualquer engajamento artificial.
- Nao burle rate limits, login, captcha, termos de uso ou permissoes de app.
- Nao envie spam nem DM fria em massa. Directs exigem conversa iniciada, opt-in, lead existente ou fluxo claramente autorizado.
- Nao publique informacao privada, dado sensivel, documento, token, conversa privada ou informacao de terceiro sem autorizacao.
- Nao crie prova social falsa, promessas garantidas, depoimentos inventados ou claims sem base.
- Nao delete conteudo, altere bio, altere link principal, bloqueie usuario real ou mude identidade visual central sem aprovacao, exceto spam/golpe evidente quando permitido.
- Nao ultrapasse orcamento, CPA maximo, ROAS minimo, regioes ou publicos aprovados.
- Em temas regulados ou sensiveis, peca aprovacao humana antes de publicar ou anunciar.

## Manifesto De Configuracao

Quando a skill for usada pela primeira vez para uma marca, monte ou atualize este manifesto:

```yaml
brand:
  name:
  niche:
  offer:
  audience:
  region:
  tone:
  prohibited_words: []
  allowed_claims: []
  proof_assets: []
accounts:
  instagram:
  tiktok:
  youtube:
  facebook:
  linkedin:
  x:
  threads:
autonomy:
  mode: assisted
  allowed_live_actions: []
  approval_required_for: []
ads:
  daily_budget_limit:
  weekly_budget_limit:
  monthly_budget_limit:
  max_cpa:
  min_roas:
  allowed_platforms: []
  allowed_objectives: []
  prohibited_categories: []
community:
  allow_comment_replies: true
  allow_dm_replies: true
  allow_proactive_dm: false
  escalation_keywords: []
reporting:
  daily_summary: true
  weekly_report: true
  action_log_path:
```

Se valores criticos estiverem vazios, use modo rascunho para a parte afetada.

## Ciclo Operacional

Para rotinas recorrentes, siga este ciclo:

1. Coletar metricas e pendencias.
2. Classificar comentarios, DMs, oportunidades e riscos.
3. Responder interacoes simples dentro das regras.
4. Separar itens sensiveis para aprovacao.
5. Identificar conteudos vencedores e lacunas de pauta.
6. Criar ou agendar conteudos.
7. Revisar campanhas de Ads ativas.
8. Pausar, ajustar ou escalar campanhas dentro dos limites.
9. Registrar acoes e gerar relatorio.

## Saida Padrao

Ao concluir uma rotina, responda:

```text
Resumo:
[Acoes principais executadas ou preparadas.]

Conteudos:
[Criados, publicados, agendados ou aguardando aprovacao.]

Comunidade:
[Comentarios/DMs respondidos, moderados ou escalados.]

Ads:
[Campanhas criadas, pausadas, otimizadas, gastos e aprovacoes pendentes.]

Metricas:
[Principais numeros e leitura objetiva.]

Riscos/Bloqueios:
[Credenciais ausentes, limites, politicas ou aprovacoes necessarias.]

Proximos passos:
[Acoes recomendadas.]
```
