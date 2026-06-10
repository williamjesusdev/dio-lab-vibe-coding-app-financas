# Plano — Vibe Wallet MVP

App web responsivo de finanças pessoais conversacional. Uma única conversa contínua, sem persistência em backend (LocalStorage), respostas do bot diretas e neutras.

## Escopo

**MUST HAVE**
- Chat em linguagem natural para registrar receitas e despesas
- Parser local (regex + dicionário) que extrai valor, tipo e categoria
- Dashboard reativo: Saldo, Receitas, Despesas, gráfico de rosca por categoria

**SHOULD HAVE**
- Criação de metas via chat ("meta de 500 para viagem") com barra de progresso

**OUT**
- Mensagens divertidas/sarcásticas do bot
- Múltiplas conversas / threads
- Integração bancária real
- Autenticação (LocalStorage só, single user)

## UI / UX

- Dark mode grafite. Verde-neon para receitas, coral/vermelho para despesas, accent roxo suave para metas
- Layout AI Elements:
  - Desktop: split — chat à esquerda (~60%), dashboard fixo à direita (~40%)
  - Mobile: dashboard compacto colapsável no topo + chat ocupando tela, composer fixo no rodapé
- Empty state amigável com 3 exemplos clicáveis ("gastei 35 no almoço", "recebi 2500 do freela", "meta de 300 para investir")
- Mensagens do usuário em bolha com fundo accent; respostas do bot sem bolha, texto direto na superfície
- Cada confirmação do bot mostra um "card de transação" inline (valor + categoria + ícone + cor)

## Arquitetura

Single-page app TanStack Start, tudo client-side. Sem Lovable Cloud nesta etapa (LocalStorage como especificado).

```
src/
  routes/
    index.tsx                 # Tela única: chat + dashboard
  components/
    ai-elements/              # Instalados via `bun x ai-elements@latest add ...`
    vibe/
      ChatPanel.tsx           # Conversation + Message + PromptInput
      Dashboard.tsx           # Saldo, totais, gráfico, metas
      TransactionCard.tsx     # Card inline em msg do bot
      GoalCard.tsx
      CategoryDonut.tsx       # Recharts
      MobileSummary.tsx       # Versão colapsada do dashboard
  lib/
    vibe/
      parser.ts               # parseMessage(text) -> Intent
      categories.ts           # Dicionário palavra→categoria + ícone+cor
      store.ts                # Zustand + persist (LocalStorage)
      types.ts
```

## Lógica do parser (client-side, sem IA)

`parseMessage(text)` retorna um dos:
- `{ kind: 'expense', amount, category, raw }`
- `{ kind: 'income', amount, category, raw }`
- `{ kind: 'goal', amount, label }`
- `{ kind: 'unknown' }`

Heurística:
1. Extrair valor: regex para números com `R$`, `reais`, vírgula/ponto. Normaliza para Number.
2. Detectar tipo:
   - Receita: verbos `recebi`, `ganhei`, `entrou`, `salário`, `freela`, `pix recebido`
   - Meta: `meta`, `quero guardar`, `objetivo`, `juntar`, `economizar`
   - Despesa: padrão (`gastei`, `paguei`, `comprei`, `almoço`, etc.) ou fallback se há valor + nenhuma palavra de receita/meta
3. Categoria: dicionário keyword→categoria
   - Alimentação 🍔: almoço, jantar, lanche, ifood, mercado, restaurante, café
   - Transporte 🚗: uber, 99, gasolina, ônibus, metrô, combustível
   - Entretenimento/Assinaturas 🎬: netflix, spotify, cinema, prime, hbo, disney
   - Moradia 🏠: aluguel, condomínio, luz, água, internet
   - Saúde 💊: farmácia, médico, consulta, remédio
   - Trabalho/Renda 💼: freela, salário, cliente, projeto
   - Outros 💸 (fallback)
4. Para metas: extrai label depois de `para` / `pra` (ex: "para viagem" → "Viagem")

Confirmações do bot (neutras):
- Despesa: "Anotado: R$ 35,00 em Alimentação."
- Receita: "Adicionado: R$ 2.500,00 em Trabalho/Renda."
- Meta: "Meta criada: R$ 300,00 para Investir."
- Unknown: "Não consegui entender. Tente: 'gastei 20 no uber' ou 'meta de 500 para viagem'."

## Estado (Zustand + persist)

```ts
{
  messages: Message[],          // {id, role, text, transactionId?, createdAt}
  transactions: Transaction[],  // {id, kind, amount, category, createdAt}
  goals: Goal[],                // {id, label, target, saved}
  // derived selectors: balance, totalIncome, totalExpense, byCategory
  send(text), reset()
}
```

Chave LocalStorage única `vibe-wallet-v1`. Reset apenas via botão "Limpar dados" no menu do dashboard.

## Dashboard

- Cards no topo: Saldo (grande), Receitas (verde-neon), Despesas (coral)
- Gráfico de rosca (Recharts) por categoria — apenas despesas, com legenda
- Seção Metas: cada meta como card com barra de progresso (`saved/target`); botão `+` adiciona valor manualmente à meta (escopo extra mínimo) — alternativamente sem botão, apenas exibe; vou incluir botão simples
- Atualização instantânea via subscribe do Zustand

## AI Elements

Instalar: `conversation`, `message`, `prompt-input`, `shimmer`.
- Mensagens assistente sem background
- Bolha do usuário com `bg-primary text-primary-foreground` (tokens custom para verde-neon suave)
- Composer com submit em `PromptInputFooter justify-end`, ícone `Send`
- Textarea com autofocus inicial e após envio
- Mensagens renderizadas via `message.parts` mesmo sem streaming (texto único part)

## Design tokens (src/styles.css)

Tokens semânticos custom:
- `--background` grafite escuro
- `--income` verde-neon, `--expense` coral, `--goal` roxo suave
- `--chat-user-bg`, `--chat-user-fg`
- Paleta do donut derivada dos tokens de categoria

Sem cores hardcoded nos componentes.

## Identidade

Logo simples gerado (carteira estilizada com glow neon) em `src/assets/vibe-logo.png`, usado no header e empty state — não usar `Sparkles`.

## Responsividade

- Header com grid `grid-cols-[minmax(0,1fr)_auto]` + `min-w-0` + `truncate`
- Breakpoint `lg`: split chat/dashboard; abaixo: dashboard colapsável (Collapsible) acima do chat
- Composer sempre fixo no bottom em mobile

## Passos de implementação

1. Definir design tokens em `src/styles.css` (cores neon, chat user)
2. Gerar logo Vibe Wallet
3. Instalar AI Elements + recharts + zustand
4. Criar `lib/vibe/`: types, categories, parser (com testes manuais via exemplos do brief), store com persist
5. Criar componentes `vibe/*`
6. Montar `routes/index.tsx` com layout split responsivo + SEO head
7. Empty state + sugestões clicáveis
8. QA: testar as 4 frases do brief + meta + responsividade mobile/desktop

## Fora do escopo

- Edição/remoção de transação individual (pode ser adicionado depois)
- Filtros por período no dashboard
- Export de dados
- Backend, auth, multi-device sync
