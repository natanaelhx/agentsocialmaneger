# Gestao De Ads

## Pre-Requisitos

Antes de criar ou alterar campanha ao vivo, exigir:

- plataforma autorizada;
- conta de anuncios;
- objetivo;
- orcamento diario/semanal/mensal;
- publico permitido;
- regioes permitidas;
- pagina de destino;
- evento de conversao;
- criativos;
- claims aprovados;
- criterio de pausa;
- criterio de escala.

Se qualquer limite financeiro estiver ausente, operar em modo rascunho.

## Plataformas

### Meta Ads

Usar Marketing API. Validar Business Manager, Ad Account, Pixel/CAPI, Page e Instagram conectados.

Objetivos comuns:

- awareness;
- traffic;
- engagement;
- leads;
- sales/conversions.

### Google Ads E YouTube Ads

Usar Google Ads API. Validar developer token, customer ID, billing ativo, conversoes e politicas.

Objetivos comuns:

- search;
- performance max;
- demand gen;
- display;
- video views;
- video action.

### TikTok Ads

Usar TikTok Business API. Validar advertiser ID, pixel/eventos, conta comercial e politicas.

Objetivos comuns:

- reach;
- traffic;
- video views;
- lead generation;
- conversions.

## Blueprint De Campanha

```yaml
campaign:
  platform:
  account_id:
  objective:
  budget_daily:
  budget_total:
  start_date:
  end_date:
  region:
  audience:
  exclusions:
  placements:
  conversion_event:
  landing_page:
  utm:
  creatives:
    - name:
      format:
      hook:
      copy:
      asset:
  pause_rules:
    max_cpa:
    min_ctr:
    max_frequency:
    max_spend_without_conversion:
  scale_rules:
    min_roas:
    max_cpa:
    min_conversions:
```

## Lancamento

1. Validar politica da plataforma.
2. Criar campanha em rascunho.
3. Validar orcamento e publico.
4. Validar criativos e destino.
5. Solicitar aprovacao se o modo nao permitir execucao ao vivo.
6. Publicar.
7. Registrar campanha, IDs e gasto previsto.

## Teste Inicial

Recomendacao padrao:

- 3 a 5 criativos por angulo;
- 2 a 4 hooks por criativo;
- janela minima de teste definida pelo volume;
- nao otimizar antes de haver dados suficientes;
- comparar criativo, publico, posicionamento e oferta.

## Otimizacao

Pausar ou revisar quando:

- CPA acima do limite apos gasto relevante;
- CTR abaixo do minimo;
- frequencia alta;
- comentarios negativos recorrentes;
- criativo rejeitado;
- destino com erro;
- gasto sem conversao acima do limite;
- ROAS abaixo da meta.

Escalar quando:

- CPA abaixo da meta;
- ROAS acima da meta;
- volume de conversoes suficiente;
- frequencia saudavel;
- criativo sem fadiga;
- comentarios sem risco relevante.

Escala deve ser gradual e dentro do teto aprovado. Nao dobrar ou multiplicar verba agressivamente sem permissao.

## Categorias Sensiveis

Pedir aprovacao humana e revisar politica antes de anunciar:

- saude;
- financas;
- politica;
- emprego;
- habitacao;
- credito;
- renda;
- emagrecimento;
- antes/depois;
- tratamentos;
- cripto;
- jogos/apostas;
- dados pessoais;
- publico menor de idade.

## Copy De Ads

Entregar sempre:

- promessa central;
- prova permitida;
- headline curta;
- primary text;
- descricao;
- CTA;
- variacoes A/B;
- risco de politica.

Evitar:

- garantia absoluta;
- vergonha corporal;
- atributos pessoais sensiveis;
- "voce tem [condicao]" quando a plataforma proibir;
- falsa urgencia;
- depoimento inventado.
