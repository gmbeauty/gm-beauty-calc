# Calculadora de Preços — GM Beauty (PWA)

Esta é a versão atualizada da sua calculadora, com salvamento automático, modo
escuro/claro, histórico, mensagens temporárias e suporte a instalação como
aplicativo (PWA). **Nenhuma fórmula ou lógica de cálculo foi alterada** — só
foram adicionadas funcionalidades e melhorias de experiência.

## Arquivos

```
index.html                  → o aplicativo (era calculadoraOK.html)
manifest.json                → configuração do PWA (nome, ícone, cor)
sw.js                        → Service Worker (funcionamento offline + auto-atualização)
icons/icon-192.png           → ícone do app (192x192)
icons/icon-512.png           → ícone do app (512x512)
icons/icon-192-maskable.png  → ícone "maskable" para Android
icons/icon-512-maskable.png  → ícone "maskable" para Android
```

Mantenha todos esses arquivos **na mesma pasta**, com esses mesmos nomes —
o `index.html` faz referência a eles por caminho relativo.

## ⚠️ Importante: como testar/hospedar

Navegadores só ativam o **Service Worker** (obrigatório para PWA e modo
offline) em dois cenários:

1. O site está em **HTTPS** (qualquer hospedagem: Netlify, Vercel, GitHub
   Pages, seu próprio domínio, etc.); ou
2. Você está testando em **localhost** (um servidor local).

Abrir o arquivo `index.html` diretamente com duplo clique (`file://...`) **não
ativa o Service Worker nem o botão de instalação**, mas o app continua
funcionando normalmente e o salvamento automático (localStorage) funciona
mesmo assim.

### Testar localmente (opcional)

Se tiver Python instalado, dentro da pasta do projeto:

```bash
python3 -m http.server 8080
```

Depois abra `http://localhost:8080` no navegador.

### Publicar de verdade

Basta subir a pasta inteira (os 4 tipos de arquivo acima) para qualquer
hospedagem estática com HTTPS. Depois de aberto uma vez, o app funciona
offline.

## O que foi adicionado

- **Salvamento automático**: qualquer alteração em qualquer campo é salva no
  `localStorage` do navegador em menos de meio segundo, sem precisar clicar
  em nada. Ao reabrir o app (mesmo depois de fechar o navegador ou desligar o
  computador), tudo volta exatamente como estava — inclusive a aba em que
  você estava e o tema (claro/escuro).
- **Mensagens temporárias (toasts)**: substituem os antigos `alert()` do
  navegador. Aparecem no canto da tela, com fade in/out, e somem sozinhas.
- **PWA completo**: manifest, ícones, Service Worker, funcionamento offline,
  atualização automática quando uma nova versão for publicada, e botão
  "Instalar app" quando o navegador permitir.
- **Indicador de conexão**: aviso discreto quando você fica offline.
- **Modo escuro/claro**: alternável pelo botão no topo, com preferência
  salva.
- **Histórico de precificações**: as últimas 20 simulações feitas na aba
  Calculadora ficam salvas numa nova aba "Histórico", com opção de limpar.
- **Botão "Limpar todos os dados"**: apaga tudo (com confirmação) e recarrega
  o app do zero.
- **Exportar cálculo em CSV**: o botão já existia na tela mas não tinha
  função associada (bug antigo) — agora funciona e baixa um `.csv` com o
  resultado calculado.
- **Indicador de "Salvando.../Salvo"**, animações suaves em campos e botões,
  spinner de carregamento inicial.

## O que **não** foi alterado

Todas as fórmulas de custo, taxas, markup, preço mínimo/sugerido e lucro
permanecem exatamente iguais (foi feita uma comparação automática confirmando
que as funções `calcularPrecos`, `simularPlataforma`, `calcularMarketplace`,
`atualizarEmbalagem`, `atualizarCustosFixos`, `atualizarResumo` e
`formatarMoeda` ficaram idênticas ao arquivo original).

## Compatibilidade

Testado para funcionar em Chrome, Edge e Firefox (desktop), além de
Android e iPhone (Safari/Chrome). No iPhone, a instalação como app é feita
por "Compartilhar → Adicionar à Tela de Início" (o Safari não usa o botão de
instalação automático do PWA).
