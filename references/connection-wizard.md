# Wizard De Conexao Agent Social Maneger

Use este wizard quando o usuario pedir para conectar redes sociais, ativar autonomia, configurar publicacao, responder comentarios/DMs, puxar metricas ou operar Ads. Siga as fases em ordem e nao pule validacoes de seguranca.

## Estado Do Wizard

Mantenha um checklist visivel durante a configuracao:

```text
Wizard Agent Social Maneger
[ ] 1. Marca e objetivo
[ ] 2. Modo de autonomia
[ ] 3. Plataformas e contas
[ ] 4. Apps de desenvolvedor
[ ] 5. OAuth e secrets
[ ] 6. Webhooks
[ ] 7. Permissoes por recurso
[ ] 8. Testes em sandbox/rascunho
[ ] 9. Manifesto final
[ ] 10. Ativacao controlada
```

## Fase 1: Marca E Objetivo

Coletar:

```yaml
brand:
  name:
  niche:
  offer:
  audience:
  region:
  tone:
  content_goals: []
  ads_goals: []
  prohibited_topics: []
  allowed_claims: []
  proof_assets: []
```

Perguntas minimas:

- Qual marca ou perfil o Zeus vai gerenciar?
- Quais plataformas entram primeiro?
- O objetivo principal e alcance, leads, vendas, autoridade ou comunidade?
- Existe alguma promessa, palavra ou tema proibido?
- Qual tom de voz deve ser usado?

## Fase 2: Modo De Autonomia

Escolher um modo:

```yaml
autonomy:
  mode: draft | assisted | controlled_autonomous
  publish_without_approval: false
  reply_comments_without_approval: true
  reply_dms_without_approval: false
  launch_ads_without_approval: false
  optimize_ads_without_approval: false
```

Padrao recomendado para primeira configuracao:

```yaml
autonomy:
  mode: assisted
  publish_without_approval: false
  reply_comments_without_approval: true
  reply_dms_without_approval: false
  launch_ads_without_approval: false
  optimize_ads_without_approval: false
```

So liberar `controlled_autonomous` depois de testes reais e limites definidos.

## Fase 3: Plataformas E Contas

Criar inventario:

```yaml
platforms:
  instagram:
    enabled: false
    handle:
    account_type: business_or_creator
    business_manager_id:
    page_id:
    instagram_business_account_id:
  facebook:
    enabled: false
    page_id:
    business_manager_id:
  youtube:
    enabled: false
    channel_id:
  tiktok:
    enabled: false
    handle:
    business_account_id:
    advertiser_id:
  google_ads:
    enabled: false
    customer_id:
    manager_customer_id:
  meta_ads:
    enabled: false
    ad_account_id:
  tiktok_ads:
    enabled: false
    advertiser_id:
  linkedin:
    enabled: false
    organization_id:
  x:
    enabled: false
    account_id:
  threads:
    enabled: false
    profile_id:
```

Validar se a conta suporta API oficial para a acao desejada. Quando a API nao suportar a acao, manter rascunho/manual assistido.

## Fase 4: Apps De Desenvolvedor

### Meta / Instagram / Facebook

Passos:

1. Criar ou selecionar app no Meta for Developers.
2. Adicionar produtos necessarios: Instagram, Facebook Login, Webhooks, Marketing API e Messenger/Instagram Messaging quando aplicavel.
3. Configurar redirect URI do OpenCloud/OpenClaw.
4. Vincular Business Manager, Page, Instagram Business/Creator e Ad Account.
5. Solicitar App Review para permissoes avancadas.

Permissoes comuns, conforme produto e API atual:

```yaml
meta_permissions:
  organic:
    - instagram_basic
    - instagram_content_publish
    - instagram_manage_comments
    - instagram_manage_insights
    - pages_show_list
    - pages_read_engagement
  messaging:
    - pages_messaging
    - instagram_manage_messages
  ads:
    - ads_management
    - ads_read
    - business_management
```

Confirmar nomes atuais nas docs da Meta antes de submeter App Review, pois a Meta muda escopos e produtos.

### Google / YouTube / Google Ads

Passos:

1. Criar projeto no Google Cloud.
2. Ativar YouTube Data API, YouTube Analytics API e Google Ads API quando necessario.
3. Configurar OAuth consent screen.
4. Criar OAuth client ID.
5. Adicionar redirect URI do OpenCloud/OpenClaw.
6. Para Google Ads, obter developer token.
7. Vincular conta Google Ads ou Manager Account.

Escopos comuns:

```yaml
google_scopes:
  youtube_upload:
    - https://www.googleapis.com/auth/youtube.upload
  youtube_manage:
    - https://www.googleapis.com/auth/youtube
    - https://www.googleapis.com/auth/youtube.force-ssl
  youtube_analytics:
    - https://www.googleapis.com/auth/yt-analytics.readonly
  google_ads:
    - https://www.googleapis.com/auth/adwords
```

Observacao: uploads do YouTube por projeto nao auditado podem ficar restritos. Tratar isso no checklist de go-live.

### TikTok / TikTok Ads

Passos:

1. Criar app no TikTok for Developers.
2. Adicionar Content Posting API.
3. Configurar Direct Post se a automacao for publicar direto.
4. Configurar redirect URI.
5. Solicitar escopos necessarios.
6. Para Ads, configurar TikTok Business API e advertiser ID.
7. Submeter audit quando precisar publicacao publica direta.

Escopos comuns:

```yaml
tiktok_scopes:
  organic:
    - user.info.basic
    - video.list
    - video.upload
    - video.publish
  ads:
    - business_api_permissions_configured_in_tiktok_business
```

Apps nao auditados podem ter restricoes de visibilidade/publicacao. Registrar isso antes de prometer publicacao automatica publica.

## Fase 5: OAuth E Secrets

Implementar endpoints por plataforma:

```text
GET  /connect/meta/start
GET  /connect/meta/callback
GET  /connect/google/start
GET  /connect/google/callback
GET  /connect/tiktok/start
GET  /connect/tiktok/callback
POST /disconnect/{platform}
GET  /connections/status
```

Fluxo:

1. Gerar `state` seguro com usuario, plataforma e nonce.
2. Redirecionar para autorizacao oficial.
3. Receber `authorization_code` no callback.
4. Validar `state`.
5. Trocar code por tokens.
6. Criptografar e salvar tokens no secret manager.
7. Salvar metadados nao sensiveis no banco.
8. Nunca logar token, refresh token ou client secret.

Modelo de storage:

```yaml
connection:
  id:
  owner_user_id:
  platform:
  account_external_id:
  account_name:
  scopes_granted: []
  token_secret_name:
  refresh_token_secret_name:
  expires_at:
  status: connected | expired | revoked | error
  created_at:
  updated_at:
```

## Fase 6: Webhooks

Criar endpoints:

```text
POST /webhooks/meta
POST /webhooks/google
POST /webhooks/tiktok
POST /webhooks/ads-events
```

Obrigatorio:

- validar assinatura da plataforma;
- deduplicar evento por ID;
- registrar evento resumido;
- enfileirar processamento;
- aplicar policy gate antes de responder ou agir;
- evitar loop de resposta.

Eventos desejados:

```yaml
webhooks:
  comments: true
  messages: true
  mentions: true
  lead_events: true
  ad_status: true
  conversion_events: true
  token_revocation: true
```

## Fase 7: Permissoes Por Recurso

Testar cada recurso separadamente:

```yaml
capability_tests:
  read_profile:
  read_metrics:
  create_draft_post:
  publish_post:
  read_comments:
  reply_comment:
  read_messages:
  reply_message:
  create_ad_draft:
  publish_ad:
  pause_ad:
  read_ad_metrics:
```

Se uma permissao falhar, marcar a capacidade como indisponivel e manter o restante funcionando.

## Fase 8: Testes Em Rascunho

Antes do go-live:

1. Puxar perfil/conexao.
2. Puxar metricas basicas.
3. Criar um post rascunho.
4. Responder um comentario de teste, se permitido.
5. Receber um webhook de teste.
6. Criar campanha de Ads em rascunho.
7. Validar logs.
8. Validar limites de orcamento.
9. Simular erro de token expirado.
10. Simular bloqueio por policy gate.

Resultado esperado:

```text
Conexao:
Plataforma:
Conta:
Escopos concedidos:
Capacidades ativas:
Capacidades bloqueadas:
Ultimo teste:
Erros:
Proximo passo:
```

## Fase 9: Manifesto Final

Gerar manifesto operacional:

```yaml
agent_social_maneger_manifest:
  version: 1
  brand:
  platforms:
  autonomy:
  allowed_actions:
    organic_publish: false
    comment_reply: true
    dm_reply: false
    proactive_dm: false
    ads_create_draft: true
    ads_publish: false
    ads_pause_on_safety_rule: true
    ads_scale: false
  budgets:
    daily:
    weekly:
    monthly:
    max_cpa:
    min_roas:
  approval_required_for:
    - new_ads_campaign
    - budget_increase
    - sensitive_topic
    - crisis_response
    - proactive_dm
    - account_profile_change
  logs:
    action_log_path:
    webhook_log_path:
  emergency:
    pause_all_ads_allowed: true
    pause_all_automation_allowed: true
```

Sem esse manifesto, nao ativar modo autonomo.

## Fase 10: Ativacao Controlada

Ativar por etapas:

1. Dia 1-3: leitura de metricas + rascunhos.
2. Dia 4-7: respostas simples em comentarios + conteudo com aprovacao.
3. Semana 2: publicacao assistida + campanhas em rascunho.
4. Semana 3: automacao controlada para acoes de baixo risco.
5. Depois: Ads e otimizacoes automaticas somente com limites e historico confiavel.

Checklist de go-live:

```text
[ ] Tokens salvos em secret manager
[ ] Refresh funcionando
[ ] Webhooks assinados e testados
[ ] Logs funcionando
[ ] Manifesto aprovado
[ ] Orcamentos definidos
[ ] Acoes sensiveis bloqueadas
[ ] Botao de emergencia definido
[ ] Primeiro relatorio gerado
```

## Saida Do Wizard

Ao terminar, responder:

```text
Wizard concluido:
Status geral:
Plataformas conectadas:
Capacidades ativas:
Capacidades em rascunho:
Aprovacoes pendentes:
Riscos:
Manifesto:
Proxima acao recomendada:
```
