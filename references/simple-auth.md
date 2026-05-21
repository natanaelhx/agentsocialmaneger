# Formas Simples De Autenticacao

Use este guia quando o usuario pedir um jeito simples de conectar as redes antes de construir um OAuth completo. A regra principal continua: nunca pedir senha da rede social e nunca salvar segredo em texto puro.

## Ordem Recomendada

1. Link de conexao OAuth pronto.
2. Token colado manualmente em um cofre seguro.
3. Chave de API quando a plataforma aceitar.
4. Device code para login guiado em terminal/TV.
5. Conta de sistema/business token para Ads e operacao server-side.
6. Modo manual assistido quando a API nao permitir automacao.

## Opcao 1: Link De Conexao OAuth

Mais simples para o usuario final.

Fluxo:

```text
Usuario clica em Conectar
-> abre tela oficial da plataforma
-> usuario autoriza
-> OpenCloud recebe callback
-> token vai para secret manager
-> Zeus testa a conexao
```

Usar para:

- Instagram/Meta;
- YouTube/Google;
- TikTok;
- LinkedIn;
- X/Twitter;
- Ads quando houver app aprovado.

Vantagem: usuario nao mexe com token.

Limite: exige app de desenvolvedor, redirect URI e aprovacao de escopos quando necessario.

## Opcao 2: Token Manual No Cofre

Mais rapido para prototipo interno.

Fluxo:

```text
Usuario gera token na plataforma
-> cola token uma unica vez no cofre/secret manager
-> Zeus salva apenas o nome do secret
-> Zeus usa o token via conector
```

Use somente quando a plataforma permitir token pessoal, token de pagina, token de business ou token de app.

Nunca colocar token em:

- prompt;
- SKILL.md;
- git;
- logs;
- planilhas abertas;
- arquivo .env commitado.

Modelo:

```yaml
manual_token_connection:
  platform:
  account_id:
  token_secret_name:
  scopes: []
  expires_at:
  refresh_method: manual | automatic
```

Vantagem: implementacao rapida.

Limite: expiracao, rotacao manual e risco maior se o cofre nao estiver correto.

## Opcao 3: API Key Simples

Usar apenas em servicos que aceitam API key para leitura, analytics, assets, agendamento ou ferramentas auxiliares. Redes sociais grandes geralmente exigem OAuth para publicar, comentar, enviar mensagem ou operar Ads.

Fluxo:

```text
Usuario cria API key
-> salva no secret manager
-> Zeus usa a key em chamadas permitidas
```

Modelo:

```yaml
api_key_connection:
  service:
  api_key_secret_name:
  allowed_actions: []
  rate_limit:
```

Vantagem: simples para ferramentas de apoio.

Limite: normalmente nao serve para agir como usuario em redes sociais.

## Opcao 4: Device Code

Bom para ambientes sem browser, CLI, servidor remoto ou TV-style login.

Fluxo:

```text
Zeus mostra um codigo
-> usuario abre uma URL oficial
-> usuario digita o codigo
-> plataforma autoriza
-> OpenCloud recebe token
```

Usar quando o provedor suportar device authorization flow.

Vantagem: nao precisa abrir callback local.

Limite: nem toda plataforma suporta, e algumas acoes sensiveis ainda exigem app review.

## Opcao 5: System User / Business Token

Melhor para operacao de Ads, paginas e contas comerciais quando a plataforma suporta usuarios de sistema ou business tokens.

Fluxo:

```text
Admin cria system user/business asset
-> concede acesso ao ativo
-> gera token com escopos minimos
-> salva token no secret manager
-> Zeus opera somente os ativos permitidos
```

Usar para:

- contas de anuncios;
- paginas;
- business managers;
- operacoes server-side;
- automacoes internas com ativos da empresa.

Vantagem: nao depende tanto de conta pessoal.

Limite: exige configuracao de negocio, permissao de admin e revisao de escopos.

## Opcao 6: Modo Manual Assistido

Usar quando a API nao permite a acao, quando o app ainda nao foi aprovado ou quando a conta nao esta pronta.

Fluxo:

```text
Zeus cria conteudo/payload
-> usuario revisa
-> usuario publica manualmente
-> Zeus registra a acao e depois analisa metricas disponiveis
```

Vantagem: funciona imediatamente.

Limite: nao e automacao completa.

## Matriz Simples De Decisao

```text
Precisa publicar/comentar/DM/Ads em nome do usuario?
-> OAuth oficial ou business token.

E so prototipo interno rapido?
-> token manual no cofre, se a plataforma permitir.

E uma ferramenta auxiliar com API key?
-> API key no cofre.

Ambiente nao tem browser/callback?
-> device code, se suportado.

API nao permite a acao?
-> modo manual assistido.
```

## Padrao Minimo De Seguranca

Sempre exigir:

- secret manager;
- escopos minimos;
- expiracao registrada;
- teste de conexao;
- log sem segredo;
- botao para desconectar;
- rotacao de token;
- bloqueio de acoes fora do manifesto.

## Teste Simples De Conexao

Depois de autenticar, rodar:

```text
1. Ler perfil da conta.
2. Confirmar ID externo.
3. Listar escopos concedidos.
4. Testar uma chamada de leitura.
5. Criar rascunho, se suportado.
6. Nao publicar nada no primeiro teste sem aprovacao.
```

Saida:

```text
Autenticacao:
Metodo:
Plataforma:
Conta:
Status:
Escopos:
Capacidades liberadas:
Capacidades bloqueadas:
Proximo passo:
```
