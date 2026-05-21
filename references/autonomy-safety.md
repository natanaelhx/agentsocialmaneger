# Autonomia, Seguranca E Governanca

## Permissao Unica Controlada

Transforme a permissao do usuario em um manifesto verificavel. A permissao deve especificar:

- contas autorizadas;
- plataformas autorizadas;
- acoes permitidas;
- tipos de conteudo permitidos;
- limites de orcamento;
- limites de DMs;
- limites de moderacao;
- temas proibidos;
- criterios de aprovacao humana;
- periodo de validade;
- caminho do log.

Sem manifesto, operar em Modo Assistido.

## Acoes Baixo Risco

Podem ser automaticas quando autorizadas:

- criar rascunhos;
- gerar calendarios;
- analisar metricas;
- responder elogios e duvidas simples;
- ocultar spam evidente;
- agendar posts aprovados;
- pausar Ads que estouraram regra de seguranca.

## Acoes Medio Risco

Exigem limites claros:

- publicar conteudo novo;
- responder objecoes comerciais;
- enviar direct em fluxo opt-in;
- redistribuir verba entre campanhas aprovadas;
- criar novas variacoes de anuncio;
- editar descricoes e legendas.

## Acoes Alto Risco

Exigem aprovacao humana:

- aumentar orcamento acima do limite;
- lancar campanha nova com gasto real sem autorizacao previa;
- deletar conteudo;
- alterar bio, nome, link principal ou identidade da conta;
- responder crise;
- lidar com tema juridico, saude, financas ou politica;
- bloquear usuario real;
- enviar comunicacao em massa;
- usar dados sensiveis.

## Log Operacional

Registrar toda acao ao vivo:

```yaml
timestamp:
agent: zeus
platform:
account:
action:
mode:
input_summary:
payload_summary:
approval_id:
estimated_spend:
actual_result:
external_id:
status:
error:
```

## Botao De Emergencia

Se houver risco de crise, gasto anormal, rejeicao repetida ou suspeita de token comprometido:

1. Pausar automacoes de publicacao e Ads quando permitido.
2. Nao apagar evidencias.
3. Registrar o incidente.
4. Gerar resumo.
5. Solicitar decisao humana.

## Privacidade

Nunca incluir em respostas ou logs:

- tokens;
- refresh tokens;
- senhas;
- documentos pessoais;
- dados financeiros completos;
- conversas privadas completas;
- informacao medica;
- dados de menores.

Use resumos minimizados sempre que possivel.

## Compliance De Conteudo

Antes de publicar ou anunciar, verificar:

- direitos de imagem;
- uso de marca de terceiro;
- claims e provas;
- politicas da plataforma;
- publico menor de idade;
- categorias sensiveis;
- regras de sorteio/promocao;
- legislacao local aplicavel.

## Falhas E Recuperacao

Se uma acao falhar:

1. Capturar erro sem expor segredo.
2. Verificar se e credencial, permissao, rate limit, politica ou payload.
3. Tentar novamente somente se for seguro e idempotente.
4. Evitar duplicar publicacao, comentario ou gasto.
5. Registrar falha e proxima acao.
