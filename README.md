# 🎓 habilite.me

> Agregador de cursos online gratuitos e pagos para brasileiros

[![Next.js](https://img.shields.io/badge/Next.js-14+-black?logo=next.js)](https://nextjs.org/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5+-blue?logo=typescript)](https://www.typescriptlang.org/)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind-3.4+-38B2AC?logo=tailwind-css)](https://tailwindcss.com/)
[![Strapi](https://img.shields.io/badge/Strapi-v5-purple?logo=strapi)](https://strapi.io/)

## 📖 Sobre

O **habilite.me** é uma plataforma que ajuda brasileiros a encontrar os melhores cursos online, sejam gratuitos ou pagos. Agregamos cursos de diversas plataformas como Udemy, YouTube, Hotmart, Gov.br, Coursera e muito mais.

### ✨ Funcionalidades

- 🔍 **Busca e filtros** - Encontre cursos por categoria, tipo, plataforma e nível
- ⭐ **Reviews** - Avaliações de usuários para ajudar na escolha
- 📝 **Blog** - Conteúdo sobre carreira, dicas de estudo e novidades
- 📱 **Responsivo** - Funciona perfeitamente em mobile, tablet e desktop
- 🚀 **Performance** - Otimizado para Core Web Vitals
- 🔎 **SEO** - Páginas otimizadas para buscadores

### 💰 Modelo de Negócio

- Links de afiliação para plataformas de cursos
- Google AdSense
- Parcerias com produtores de conteúdo

## 🛠️ Tech Stack

| Tecnologia | Uso |
|------------|-----|
| [Next.js 14+](https://nextjs.org/) | Frontend (App Router, SSR/SSG) |
| [TypeScript](https://www.typescriptlang.org/) | Tipagem estática |
| [Tailwind CSS](https://tailwindcss.com/) | Estilização |
| [Strapi v5](https://strapi.io/) | Headless CMS |
| [PostgreSQL](https://www.postgresql.org/) | Banco de dados |
| [Coolify](https://coolify.io/) | Deploy |
| [Cloudflare](https://cloudflare.com/) | CDN |

## 📁 Estrutura do Projeto

```
habilite.me/
├── apps/
│   ├── web/                # Next.js Frontend
│   │   ├── app/            # App Router pages
│   │   ├── components/     # React components
│   │   ├── lib/            # Utilities
│   │   └── types/          # TypeScript types
│   │
│   └── cms/                # Strapi CMS
│       ├── config/         # Configurações
│       └── src/api/        # Content-Types
│
├── docker/                 # Docker configs
├── docs/                   # Documentação adicional
│
├── CLAUDE.md              # Guia para IA (design system, padrões)
├── AGENTS.md              # Ponto de entrada para agentes IA
├── PLAN.md                # Plano de implementação
└── README.md              # Este arquivo
```

## 🚀 Quick Start

### Pré-requisitos

- Node.js 20+
- pnpm 8+
- PostgreSQL 16+ (ou Docker)

### Instalação

```bash
# Clone o repositório
git clone https://github.com/seu-usuario/habilite.me.git
cd habilite.me

# Instale as dependências
pnpm install

# Configure as variáveis de ambiente
cp .env.example .env.local
# Edite .env.local com suas configurações

# Inicie o banco de dados (com Docker)
docker compose up -d postgres

# Inicie o desenvolvimento
pnpm dev
```

### Scripts Disponíveis

```bash
# Desenvolvimento
pnpm dev          # Inicia todos os serviços
pnpm dev:web      # Apenas frontend (Next.js)
pnpm dev:cms      # Apenas CMS (Strapi)

# Build
pnpm build        # Build de produção
pnpm build:web    # Build do frontend
pnpm build:cms    # Build do CMS

# Qualidade
pnpm lint         # ESLint
pnpm typecheck    # TypeScript check
pnpm format       # Prettier

# Docker
pnpm docker:up    # Inicia containers
pnpm docker:down  # Para containers
```

## 🌐 URLs

| Ambiente | Frontend | CMS Admin |
|----------|----------|-----------|
| **Desenvolvimento** | http://localhost:3000 | http://localhost:1337/admin |
| **Produção** | https://habilite.me | https://cms.habilite.me/admin |

## 📚 Documentação

| Documento | Descrição |
|-----------|-----------|
| [CLAUDE.md](./CLAUDE.md) | Design system, padrões de código, prompts para IA |
| [PLAN.md](./PLAN.md) | Plano de implementação, schema do banco, roadmap |
| [AGENTS.md](./AGENTS.md) | Ponto de entrada para agentes de IA |

## 🎨 Design System

O projeto segue um design system consistente definido no [CLAUDE.md](./CLAUDE.md):

### Cores Principais

| Cor | Uso | Hex |
|-----|-----|-----|
| Primary (Verde) | Ações principais, sucesso | `#10b981` |
| Secondary (Azul) | Links, informação | `#3b82f6` |
| Accent (Amarelo) | Destaques, ratings | `#f59e0b` |

### Cores de Plataformas

| Plataforma | Hex |
|------------|-----|
| Udemy | `#a435f0` |
| YouTube | `#ff0000` |
| Hotmart | `#f04e23` |
| Gov.br | `#1351b4` |

## 🤖 Desenvolvimento com IA

Este projeto é desenvolvido em parceria com agentes de IA. Se você é um agente (Claude, Cursor, Windsurf, etc.), comece lendo:

1. **[AGENTS.md](./AGENTS.md)** - Ponto de entrada
2. **[CLAUDE.md](./CLAUDE.md)** - Design system e padrões
3. **[PLAN.md](./PLAN.md)** - Plano de implementação

## 📊 Métricas de Qualidade

### Performance (Target)

| Métrica | Target |
|---------|--------|
| LCP | < 2.5s |
| FID | < 100ms |
| CLS | < 0.1 |
| PageSpeed Mobile | 90+ |

### SEO

- Todas as páginas com `generateMetadata()`
- JSON-LD Schema.org em páginas de cursos e posts
- Sitemap dinâmico
- robots.txt configurado

### Acessibilidade

- WCAG 2.1 AA compliance
- Navegação por teclado
- Screen reader friendly
- Contraste mínimo 4.5:1

## 🗺️ Roadmap

- [x] Planejamento e documentação
- [ ] **Fase 1:** Setup (infraestrutura, deploy)
- [ ] **Fase 2:** Frontend base (design system, layout)
- [ ] **Fase 3:** Páginas de cursos
- [ ] **Fase 4:** SEO e meta tags
- [ ] **Fase 5:** Blog
- [ ] **Fase 6:** Reviews e formulários
- [ ] **Fase 7:** Lançamento MVP

## 🤝 Contribuição

Este é um projeto privado no momento. Para mais informações sobre contribuição, entre em contato.

## 📄 Licença

Todos os direitos reservados © 2025 habilite.me

---

<p align="center">
  Feito com 💚 para ajudar brasileiros a se qualificarem
</p>
