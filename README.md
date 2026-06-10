---

# 💬 Vibe Wallet

### 📱 App de Finanças Pessoais Conversacional

## 🛠️ Link do App

👉 [https://vibe-talk-wallet.lovable.app](https://vibe-talk-wallet.lovable.app)

---

## 📖 Resumo do App

O **Vibe Wallet** é um aplicativo de **finanças pessoais com interface conversacional**, onde os usuários podem controlar seus gastos e metas de forma natural — como se estivessem conversando com um assistente financeiro.

Os principais diferenciais são:

* Registro de gastos usando linguagem natural
* Classificação automática das transações
* Organização de metas financeiras
* Relatórios simples e intuitivos
* Interface conversa-style, sem formulários complexos

O objetivo é tornar o controle financeiro **acessível até para pessoas que nunca usaram um app desse tipo**.

---

## 📌 Prompt Final (PRD)

```markdown
Atue como um Engenheiro de Software Sênior e Especialista em UI/UX. Quero que você crie o MVP de um aplicativo web responsivo chamado [Vibe Wallet]. É um app de finanças pessoais conversacional.

### 1. Visão Geral e Objetivo
- **Problema:** Usuários desistem de controlar finanças por causa de formulários manuais complexos.
- **Objetivo:** Reduzir o esforço de registro criando uma interface de chat estilo "mensageiro" (WhatsApp/Telegram), onde o usuário lança seus movimentos usando linguagem natural.
- **Público-Alvo:** Desde jovens estudantes até trabalhadores autônomos que buscam praticidade e zero termos técnicos.

### 2. Interface do Usuário (UI/UX - A Vibe)
- **Tema:** Dark mode elegante (fundo grafite/escuro) com elementos vibrantes em verde-neon (para receitas) e vermelho/coral (para despesas).
- **Layout de Mensageiro:** Uma tela dividida ou um layout limpo com uma área de histórico de mensagens no centro e um campo de texto fixo na parte inferior com o botão "Enviar".
- **Componente Visual Auxiliar:** Na lateral (ou topo, se mobile), mostre um pequeno Dashboard que se atualiza em tempo real: Saldo Atual, Receitas, Despesas e uma barra de progresso para "Metas".

### 3. Funcionalidades do MVP (Escopo MoSCoW)
- **MUST HAVE (Obrigatório):**
  1. Registro de transações via chat em linguagem natural.
  2. Categorização automática baseada na mensagem.
  3. Painel visual (Dashboard) com saldo e gráfico básico de pizza/rosca por categoria.
- **SHOULD HAVE (Desejável):**
  1. Criação de metas simples através do chat (ex: "Quero guardar R$ 500 para viagem"). Uma barra de progresso visual deve aparecer no dashboard.
- **COULD HAVE (Se houver tempo):**
  1. Uma mensagem de feedback da IA dando uma dica divertida (ex: se gastar com fast-food, o bot diz: "Mais um lanche? Sua carteira vai chorar, hein! 😂").
- **WON'T HAVE:** Integração com bancos reais (tudo deve ser simulado localmente).

### 4. Inteligência do Chat (Simulação de Linguagem Natural)
Implemente uma lógica em JavaScript/TypeScript no front-end para capturar o texto digitado pelo usuário e identificar: Valor, Tipo (Receita/Despesa) e Categoria. 

**Exemplos de frases que o sistema DEVE entender e processar:**
- *Usuário:* "gastei 35 reais no almoço" -> *Ação:* Adicionar Despesa, R$ 35.00, Categoria: Alimentação. *Resposta do Bot:* "Entendido! R$ 35,00 anotados em Alimentação. 🍔"
- *Usuário:* "recebi 2500 do freela" -> *Ação:* Adicionar Receita, R$ 2500.00, Categoria: Trabalho/Renda. *Resposta do Bot:* "Aí sim! R$ 2.500,00 adicionados ao seu saldo. 💰"
- *Usuário:* "paguei 40 reais da netflix" -> *Ação:* Adicionar Despesa, R$ 40.00, Categoria: Entretenimento/Assinaturas.
- *Usuário:* "meta de 300 reais para investir" -> *Ação:* Atualizar/Criar meta com valor alvo de R$ 300.

### 5. Requisitos Não-Funcionais
- **Responsividade:** Deve ser perfeito no celular (foco principal) e desktop.
- **Feedback Visual Instantâneo:** Assim que o usuário der "Enter" no chat, o saldo e os gráficos no Dashboard devem se mover e atualizar de forma fluida (em até 1-2 segundos).
- **Persistência Simples:** Armazene os dados no LocalStorage do navegador para que o usuário não perca as informações ao atualizar a página.
```

---

## 🤔 Reflexão sobre o Processo

### ✅ O que funcionou bem

* A **experiência conversacional** simplificou o registro de gastos e deixou o fluxo mais natural.
* O **PRD ajudou a organizar ideias** e estruturar o MVP de forma clara.
* O **Plan Mode** do Lovable ajudou com perguntas cruciais na definição do MVP [/vibe_wallet_plan.md](https://github.com/williamjesusdev/dio-lab-vibe-coding-app-financas/blob/main/vibe_wallet_plan.md).
* A interação com a IA acelerou muito a documentação do projeto.

---

### ⚠️ O que não funcionou como esperado

* A **categorização automática** ainda precisa de ajustes para evitar algumas classificações erradas.
* Algumas interações podem ser **mais intuitivas para usuários que nunca usaram apps de finanças**.

---

### 🧠 O que aprendi sobre conversar com IAs

* **Detalhar bem o prompt** ajuda a receber respostas mais úteis e organizadas.
* A interação é mais produtiva quando o objetivo está **muito claro e específico**.
* Conversar com IA pode **acelerar prototipação de ideias e documentação** de projetos complexos.

---

## 🔚 Conclusão

O **Vibe Wallet** é uma proposta inovadora de finanças pessoais usando linguagem natural em vez de formulários tradicionais.
O uso de IA transformou o processo de documentação e desenvolvimento de ideias, tornando essa ferramenta valiosa para projetos futuros.
