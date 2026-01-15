# AGENTS.md - habilite.me

Este arquivo serve como ponto de entrada para agentes de IA (Claude, Claude Code, Cursor, Windsurf, Jules, Antigravity, etc.) que trabalham neste projeto.

## 📖 Documentação Principal

**Leia o arquivo [`CLAUDE.md`](./CLAUDE.md) para:**

- Design System completo (cores, tipografia, espaçamento)
- Stack tecnológico
- Padrões de código
- Prompts base para desenvolvimento
- Workflows de desenvolvimento
- Checklists de validação

## 📋 Plano de Implementação

**Leia o arquivo [`PLAN.md`](./PLAN.md) para:**

- Arquitetura do sistema
- Schema do banco de dados (Strapi)
- Estrutura de páginas
- Roadmap de execução
- Configuração de deploy

## 🎯 Resumo Rápido

| Aspecto | Tecnologia |
|---------|------------|
| **Frontend** | Next.js 14+ (App Router), TypeScript, Tailwind CSS |
| **CMS** | Strapi v5 |
| **Database** | PostgreSQL 16 |
| **Deploy** | Coolify + Cloudflare |

## ⚡ Comandos Rápidos

```bash
# Desenvolvimento
pnpm dev          # Inicia frontend e CMS
pnpm dev:web      # Apenas frontend
pnpm dev:cms      # Apenas Strapi

# Build
pnpm build        # Build de produção
pnpm lint         # Linting
pnpm typecheck    # Verificação de tipos
```

## 🚨 Regras Importantes

1. **Server Components por padrão** - Use Client Components apenas quando necessário
2. **TypeScript strict** - Nunca use `any`
3. **Mobile-first** - Comece sempre pelo mobile
4. **Acessibilidade** - WCAG 2.1 AA obrigatório
5. **SEO** - Todas as páginas precisam de `generateMetadata()` e JSON-LD
6. **Performance** - Target: LCP < 2.5s, CLS < 0.1

---

**→ Comece lendo o [`CLAUDE.md`](./CLAUDE.md)**
