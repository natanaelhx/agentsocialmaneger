# Integracoes E Conectores

## Principios

Use apenas integracoes oficiais e autorizadas. Antes de implementar ou executar codigo contra uma plataforma, verifique a documentacao oficial atual da API, escopos OAuth, permissoes do app, limites de taxa e recursos disponiveis para o tipo de conta.

Quando nao houver conector ao vivo no OpenCloud/OpenClaw, entregue:

- lista de credenciais necessarias;
- escopos OAuth;
- endpoints oficiais provaveis;
- payloads de exemplo;
- riscos e limitacoes;
- plano de implementacao.

## Inventario De Credenciais

Nunca armazene senha em texto puro. Preferir secret manager, variaveis de ambiente criptografadas ou cofre do OpenCloud/OpenClaw.

Campos comuns:

```yaml
meta:
  app_id:
  app_secret_secret_name:
  access_token_secret_name:
  business_manager_id:
  ad_account_id:
  page_id:
  instagram_business_account_id:
google:
  developer_token_secret_name:
  oauth_client_id:
  oauth_client_secret_secret_name:
  refresh_token_secret_name:
  customer_id:
  analytics_property_id:
youtube:
  channel_id:
  oauth_scopes: []
tiktok:
  app_id:
  client_key:
  client_secret_secret_name:
  advertiser_id:
  business_account_id:
linkedin:
  organization_id:
  access_token_secret_name:
x:
  api_key_secret_name:
  api_secret_secret_name:
  access_token_secret_name:
threads:
  profile_id:
  access_token_secret_name:
```

## Capacidades Por Plataforma

### Instagram / Facebook / Meta

Use Meta Graph API, Instagram Graph API, Messenger API e Marketing API quando a conta e o app tiverem permissao.

Validar:

- conta Instagram Business ou Creator conectada a uma Page;
- permissoes para publicar midia, ler insights, gerenciar comentarios e mensagens;
- Page ID, Instagram Business Account ID, Business Manager ID e Ad Account ID;
- webhooks para comentarios, mensagens e eventos.

Acoes comuns:

- publicar foto, video, reel e carrossel quando suportado pela API;
- responder, ocultar ou moderar comentarios;
- ler insights de midia e conta;
- criar e gerenciar campanhas no Meta Ads;
- responder mensagens via Messenger/Instagram Messaging API quando autorizado.

### YouTube

Use YouTube Data API e YouTube Analytics API.

Acoes comuns:

- enviar videos;
- atualizar titulo, descricao, tags e thumbnails;
- ler e responder comentarios;
- coletar metricas de canal e videos;
- operar YouTube Ads via Google Ads quando configurado.

Publicacoes de comunidade e alguns recursos podem ter restricoes especificas. Verificar suporte atual antes de prometer execucao.

### TikTok

Use TikTok Content Posting API e TikTok Business API conforme permissao da conta/app.

Acoes comuns:

- publicar ou preparar videos;
- consultar metricas disponiveis;
- gerenciar campanhas no TikTok Ads;
- responder comentarios somente se API e permissao estiverem disponiveis.

Nem todos os recursos de app consumer estao disponiveis para automacao. Se a API nao suportar uma acao, entregar rascunho e instrucoes de publicacao.

### LinkedIn

Use LinkedIn Marketing API e endpoints de organizacao autorizados.

Acoes comuns:

- publicar em perfil/organizacao quando permitido;
- coletar metricas de posts e pagina;
- criar campanhas LinkedIn Ads se a conta tiver permissao.

### X/Twitter

Use API oficial da X com plano e permissoes adequadas.

Acoes comuns:

- publicar posts;
- responder mencoes;
- coletar metricas disponiveis;
- evitar automacoes agressivas, replies em massa e comportamento que pareca spam.

### Threads

Use API oficial quando disponivel para a conta/app. Confirmar escopos, limites e tipos de midia suportados antes de publicar.

## Webhooks

Configurar webhooks para:

- novos comentarios;
- novas mensagens;
- mencoes;
- eventos de lead;
- conversoes;
- mudancas de status de campanha;
- rejeicoes de anuncio.

Todo webhook deve validar assinatura, deduplicar eventos, registrar payload resumido e evitar responder duas vezes ao mesmo evento.

## Modo Degradado

Se uma API nao estiver disponivel ou credencial estiver ausente:

1. Nao simule sucesso.
2. Gere o conteudo ou payload.
3. Liste a permissao ausente.
4. Explique o proximo passo tecnico.
5. Mantenha a acao em rascunho.
