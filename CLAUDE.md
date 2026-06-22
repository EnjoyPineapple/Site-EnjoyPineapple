# CLAUDE.md — Site Enjoy Pineapple

Contexto completo para o Claude Web continuar o desenvolvimento do site sem perder histórico.

---

## O QUE É ESTE PROJETO

Site institucional da **Enjoy Pineapple** (enjoypineapple.com.br), empresa fundada por Pablo (Porto Alegre/RS).
CNPJ: 23.904.939/0001-86

**Propósito:** Apresentar a empresa e o app BORA, capturar leads de parceiros e redirecionar para as páginas legais do app.

**Hospedagem:** GitHub Pages com domínio customizado via `CNAME` → `enjoypineapple.com.br`

**Repositório:** https://github.com/EnjoyPineapple/Site-EnjoyPineapple

---

## STACK TÉCNICA

- **HTML/CSS/JavaScript puro** — sem framework, sem build, sem npm
- **Supabase** — backend para formulário de waitlist/parceiros
  - URL: `https://pxyoazvomvterolknyoe.supabase.co`
  - Tabela: `tb_waitlist` (campos: nome, email, perfil)
  - SDK carregado via CDN: `@supabase/supabase-js@2`
- **Google Fonts** — Bebas Neue, Syne, DM Mono, Inter
- **GitHub Pages** — deploy automático ao fazer push em master

---

## DESIGN SYSTEM

### Cores (CSS variables em :root)
```css
--bg: #07090c          /* fundo principal */
--bg2: #0c1017         /* fundo alternado (seções) */
--surface: #141d28     /* cards */
--accent: #FFD600      /* amarelo — cor principal da marca */
--text: #f0f4f8        /* texto principal */
--text2: #8a9bac       /* texto secundário */
--text3: #4a5c6c       /* texto terciário / placeholder */
--green: #00e5a0
--red: #ff5f5f
--blue: #3b9eff
```

### Fontes
- `Bebas Neue` → títulos grandes (h1, h2, logos)
- `Syne` → subtítulos e destaques
- `DM Mono` → labels, badges, código
- `Inter` → corpo de texto

### Tema
Dark mode total. Nunca usar fundo branco.

---

## ESTRUTURA DE ARQUIVOS

```
index.html          → página principal (landing page)
parceiros.html      → página de parceiros com formulário
privacidade.html    → política de privacidade
termos.html         → termos de uso
suporte.html        → página de suporte
contrato.html       → modelo de contrato de parceria
admin.html          → painel admin (autenticação Supabase)
CNAME               → enjoypineapple.com.br

assets/
  enjoypineapple.jpeg   → logo circular preto e branco
  icon.png              → ícone do app BORA
  screen1.png           → screenshot: tela de busca do BORA
  screen2.png           → screenshot: tela de resultado/classificação
  screen3.png           → screenshot: tela de legislação
  screen4.png           → screenshot: tela de parceiros
  sectors/
    agro.jpg            → foto setor agronegócio
    comercio.jpg        → foto setor comércio
    const.jpg           → foto setor construção
    indu.jpg            → foto setor indústria
    servi.jpg           → foto setor serviços
    transporte.jpg      → foto setor transporte
```

---

## SEÇÕES DO INDEX.HTML (em ordem)

1. **NAV** — logo + links (Sobre, BORA, Parceiros, CTA "Seja um Parceiro")
2. **HERO** — carousel de fundo com fotos dos 6 setores + headline + botões
3. **MVV** (#sobre) — Missão, Visão, Valores em 3 cards
4. **PRODUTO: BORA** (#bora) — logo do app, descrição, badges Play Store / App Store (iOS em breve), 4 screenshots do app
5. **COMO FUNCIONA** — 3 passos: município → busca → resultado
6. **PARA QUEM** (#para-quem) — 5 cards: Empresários, Contadores, Advogados, Empreendedores, Arquitetos/Engenheiros
7. **SEJA UM PARCEIRO** (#parceiro) — 4 tipos: Contabilidades, Jurídico, Ambiental, Benefícios
8. **WAITLIST** (#waitlist) — CTA para parceiros com link para parceiros.html
9. **FOOTER** — logo, CNPJ, links de navegação, copyright

---

## O APP BORA (contexto do produto apresentado no site)

- App mobile Android (React Native + Expo)
- **Publicado na Google Play Store** em fase de testes com testadores
- iOS em breve (badge "Em breve na App Store" no site)
- **O que faz:** classificação de risco de atividades econômicas por CNAE e município
- Backend: Supabase
- Outro repositório: https://github.com/EnjoyPineapple/app_BORA

---

## OUTROS PRODUTOS DA EMPRESA

- **Divide Aí** — app de divisão de despesas entre amigos
  - React Native + Expo + AsyncStorage (sem backend)
  - Repositório: https://github.com/EnjoyPineapple/app_divide_ai
  - Status: em desenvolvimento

---

## COMPORTAMENTOS IMPORTANTES

- O `index.html` tem um script no topo que redireciona tokens Supabase para `admin.html` (autenticação via magic link)
- O formulário de waitlist insere em `tb_waitlist` e trata duplicidade (código 23505)
- O carousel de fundo do hero troca automaticamente a cada 3,5 segundos com suporte a swipe touch
- Animações de entrada via IntersectionObserver (fade-in com translateY)
- Responsivo: breakpoint em 900px (nav some, grid vira coluna única)

---

## O QUE PODE SER MELHORADO (pendências conhecidas)

- [ ] Link real da Play Store (atualmente aponta para play.google.com/store sem URL do app)
- [ ] Página de parceiros (`parceiros.html`) — verificar se formulário está funcional
- [ ] Mobile: nav sem menu hamburguer (links somem em telas pequenas)
- [ ] Admin (`admin.html`) — painel de gestão dos leads/parceiros

---

## COMO FAZER DEPLOY

Qualquer push na branch `master` do repositório `Site-EnjoyPineapple` atualiza automaticamente o site em `enjoypineapple.com.br` via GitHub Pages.

```bash
git add .
git commit -m "descrição da mudança"
git push origin master
```

