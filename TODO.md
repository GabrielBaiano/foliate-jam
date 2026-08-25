# 📋 Paperback - Roadmap & TODO

Este documento rastreia as melhorias, novas funcionalidades, otimizações de performance e correções planejadas para o **Paperback**.

---

## ⚡ Fase 0: Performance & Arquitetura (Backend, DB & WebSockets)

- [x] **Modo WAL no SQLite & Otimização de Concorrência**
  - *Descrição:* Configurar `PRAGMA journal_mode = WAL;` e `PRAGMA synchronous = NORMAL;` para evitar locks de tabela durante leituras/escritas concorrentes.
  - *Arquivos envolvidos:* [`db.js`](file:///home/gabrielgama/.gemini/antigravity/scratch/paperback/db.js)
- [x] **Índices no Banco de Dados SQLite**
  - *Descrição:* Adicionar índices explícitos para `room_id`, `discord_id` e `last_active` nas tabelas `room_members`, `highlights` e `rooms`.
  - *Arquivos envolvidos:* [`db.js`](file:///home/gabrielgama/.gemini/antigravity/scratch/paperback/db.js)
- [x] **Throttling de Cursor ao Vivo via WebSockets**
  - *Descrição:* Aplicar throttling de 30-50ms na transmissão dos eventos `mousemove` do cursor dos leitores.
  - *Arquivos envolvidos:* [`bookclub.js`](file:///home/gabrielgama/.gemini/antigravity/scratch/paperback/bookclub.js), [`server.js`](file:///home/gabrielgama/.gemini/antigravity/scratch/paperback/server.js)
- [x] **Batching / Debounce de Posição (`handleRelocate`)**
  - *Descrição:* Manter a posição em memória e agrupar atualizações no banco SQLite para reduzir IO excessivo em navegação rápida.
  - *Arquivos envolvidos:* [`server.js`](file:///home/gabrielgama/.gemini/antigravity/scratch/paperback/server.js)
- [x] **Eliminação de Chamadas N+1 ao Supabase Storage**
  - *Descrição:* Otimizar checagem de existência do arquivo EPUB no endpoint `/api/my-rooms` armazenando o estado na tabela `rooms` em vez de chamar `.list()` em loop.
  - *Arquivos envolvidos:* [`server.js`](file:///home/gabrielgama/.gemini/antigravity/scratch/paperback/server.js)

---

## 🚪 Fase 1: Onboarding e Experiência Inicial (UX)

- [ ] **Modo Convidado ("Read as Guest")**
  - *Descrição:* Permitir criar salas e entrar em salas sem obrigatoriedade imediata de login com o Discord, reduzindo a fricção inicial de novos leitores.
  - *Arquivos envolvidos:* [`server.js`](file:///home/gabrielgama/.gemini/antigravity/scratch/paperback/server.js), [`bookclub.js`](file:///home/gabrielgama/.gemini/antigravity/scratch/paperback/bookclub.js), [`reader.html`](file:///home/gabrielgama/.gemini/antigravity/scratch/paperback/reader.html)
- [ ] **Banner de Vinculação de Perfil Discord**
  - *Descrição:* Exibir opção para o leitor convidado migrar para uma conta Discord salva sem perder seu progresso ou destaques.
  - *Arquivos envolvidos:* [`bookclub.js`](file:///home/gabrielgama/.gemini/antigravity/scratch/paperback/bookclub.js), [`reader.html`](file:///home/gabrielgama/.gemini/antigravity/scratch/paperback/reader.html)

---

## 🎨 Fase 2: Personalização Tipográfica e Temas Visuais

- [ ] **Seletor de Família de Fontes (Font Family)**
  - *Descrição:* Alternar entre Serif (Merriweather/Georgia), Sans-Serif (Inter), Monospace, OpenDyslexic e Padrão da Editora.
  - *Arquivos envolvidos:* [`reader.js`](file:///home/gabrielgama/.gemini/antigravity/scratch/paperback/reader.js), [`reader.html`](file:///home/gabrielgama/.gemini/antigravity/scratch/paperback/reader.html)
- [ ] **Ajuste de Margens Laterais e Largura da Coluna**
  - *Descrição:* Permitir alterar a largura útil do texto (Estrita, Normal, Larga).
  - *Arquivos envolvidos:* [`paginator.js`](file:///home/gabrielgama/.gemini/antigravity/scratch/paperback/paginator.js), [`reader.js`](file:///home/gabrielgama/.gemini/antigravity/scratch/paperback/reader.js)
- [ ] **Novos Temas Visuais de Leitura**
  - *Descrição:* Adicionar temas OLED Black (`#000000`), Warm Parchment (Sepia suave) e Solarized Dark.
  - *Arquivos envolvidos:* [`reader.js`](file:///home/gabrielgama/.gemini/antigravity/scratch/paperback/reader.js), [`reader.html`](file:///home/gabrielgama/.gemini/antigravity/scratch/paperback/reader.html), [`bookclub.css`](file:///home/gabrielgama/.gemini/antigravity/scratch/paperback/bookclub.css)

---

## 🤝 Fase 3: Recursos Colaborativos Avançados & Modos de Leitura

- [ ] **Modo "Seguir o Anfitrião" (Leader / Follower Mode)**
  - *Descrição:* Permitir que leitores sincronizem a tela com o host/mediador do clube do livro.
  - *Arquivos envolvidos:* [`bookclub.js`](file:///home/gabrielgama/.gemini/antigravity/scratch/paperback/bookclub.js), [`server.js`](file:///home/gabrielgama/.gemini/antigravity/scratch/paperback/server.js)
- [ ] **Reações com Emojis nos Destaques (❤️, 💡, 🤯, 📚)**
  - *Descrição:* Permitir que os leitores reajam aos destaques uns dos outros.
  - *Arquivos envolvidos:* [`bookclub.js`](file:///home/gabrielgama/.gemini/antigravity/scratch/paperback/bookclub.js), [`server.js`](file:///home/gabrielgama/.gemini/antigravity/scratch/paperback/server.js)
- [ ] **Drawer / Bottom Sheet Responsivo para Mobile**
  - *Descrição:* Painel lateral transformado em gaveta deslizante inferior em dispositivos móveis.
  - *Arquivos envolvidos:* [`bookclub.css`](file:///home/gabrielgama/.gemini/antigravity/scratch/paperback/bookclub.css), [`reader.html`](file:///home/gabrielgama/.gemini/antigravity/scratch/paperback/reader.html)

---

## ✍️ Fase 4: Anotações, Exportação & Estudo

- [ ] **Gerador de Imagem de Citação (Quote Cards)**
  - *Descrição:* Criar cartões com trechos estilizados do livro com marca d'água para compartilhamento em redes sociais.
  - *Arquivos envolvidos:* [`quote-image.js`](file:///home/gabrielgama/.gemini/antigravity/scratch/paperback/quote-image.js), [`reader.js`](file:///home/gabrielgama/.gemini/antigravity/scratch/paperback/reader.js)
- [ ] **Exportação de Destaques e Anotações (Markdown / Notion)**
  - *Descrição:* Exportar marcadores e notas coletivas em Markdown, TXT ou JSON.
  - *Arquivos envolvidos:* [`reader.js`](file:///home/gabrielgama/.gemini/antigravity/scratch/paperback/reader.js)

---

## 🎧 Fase 5: Leitura Avançada & Integrações

- [ ] **Discord Embedded App (Discord Activity SDK)**
  - *Descrição:* Integrar o SDK de Atividades do Discord para rodar o Paperback nativamente dentro de canais de voz.
  - *Arquivos envolvidos:* [`server.js`](file:///home/gabrielgama/.gemini/antigravity/scratch/paperback/server.js), [`reader.html`](file:///home/gabrielgama/.gemini/antigravity/scratch/paperback/reader.html)
- [ ] **Suporte a Formatos Adicionais (MOBI, PDF, CBZ/Mangás)**
  - *Descrição:* Liberar upload e leitura de PDF, MOBI e arquivos CBZ para quadrinhos/mangás.
  - *Arquivos envolvidos:* [`server.js`](file:///home/gabrielgama/.gemini/antigravity/scratch/paperback/server.js), [`reader.js`](file:///home/gabrielgama/.gemini/antigravity/scratch/paperback/reader.js)
