# CLAUDE.md - habilite.me
## Guia para Desenvolvimento com IA

---

## 📋 ÍNDICE

1. [Visão Geral](#visão-geral)
2. [Design System](#design-system)
3. [Stack Tecnológico](#stack-tecnológico)
4. [Agentes Especializados](#agentes-especializados)
5. [Prompts Base](#prompts-base)
6. [Workflows de Desenvolvimento](#workflows-de-desenvolvimento)
7. [Padrões de Código](#padrões-de-código)
8. [Testes e Validação](#testes-e-validação)

---

## 🎯 VISÃO GERAL

Este documento define como usar agentes de IA (Claude, Claude Code, Jules, Antigravity) para desenvolver e manter o habilite.me seguindo um design system consistente e stack tecnológico otimizado.

**Filosofia:**
- Agentes desenvolvem código profissional, seguro e performático
- Design system garante consistência visual
- Código modular e reutilizável
- SEO e Performance desde o início (Core Web Vitals)
- Acessibilidade WCAG 2.1 AA
- Mobile-first, responsivo
- TypeScript strict mode sempre

**Sobre o Projeto:**
- **Domínio:** habilite.me
- **Objetivo:** Agregador de cursos gratuitos e pagos para brasileiros
- **Modelo:** Afiliação + AdSense (sem cursos próprios)
- **Público:** Brasileiros buscando qualificação profissional

---

## 🎨 DESIGN SYSTEM

### Identidade Visual

O habilite.me tem uma identidade **moderna, confiável e acessível**, voltada para brasileiros que buscam desenvolvimento profissional. A marca transmite crescimento, educação e oportunidade.

### Paleta de Cores

```css
:root {
  /* ========================================
     PRIMARY - Verde Crescimento/Educação
     ======================================== */
  --color-primary-50: #ecfdf5;
  --color-primary-100: #d1fae5;
  --color-primary-200: #a7f3d0;
  --color-primary-300: #6ee7b7;
  --color-primary-400: #34d399;
  --color-primary-500: #10b981;  /* Principal */
  --color-primary-600: #059669;
  --color-primary-700: #047857;
  --color-primary-800: #065f46;
  --color-primary-900: #064e3b;
  --color-primary-950: #022c22;

  /* ========================================
     SECONDARY - Azul Confiança
     ======================================== */
  --color-secondary-50: #eff6ff;
  --color-secondary-100: #dbeafe;
  --color-secondary-200: #bfdbfe;
  --color-secondary-300: #93c5fd;
  --color-secondary-400: #60a5fa;
  --color-secondary-500: #3b82f6;  /* Principal */
  --color-secondary-600: #2563eb;
  --color-secondary-700: #1d4ed8;
  --color-secondary-800: #1e40af;
  --color-secondary-900: #1e3a8a;
  --color-secondary-950: #172554;

  /* ========================================
     ACCENT - Amarelo Destaque
     ======================================== */
  --color-accent-50: #fffbeb;
  --color-accent-100: #fef3c7;
  --color-accent-200: #fde68a;
  --color-accent-300: #fcd34d;
  --color-accent-400: #fbbf24;
  --color-accent-500: #f59e0b;  /* Principal */
  --color-accent-600: #d97706;
  --color-accent-700: #b45309;
  --color-accent-800: #92400e;
  --color-accent-900: #78350f;
  --color-accent-950: #451a03;

  /* ========================================
     NEUTRAL - Cinzas
     ======================================== */
  --color-neutral-50: #fafafa;
  --color-neutral-100: #f4f4f5;
  --color-neutral-200: #e4e4e7;
  --color-neutral-300: #d4d4d8;
  --color-neutral-400: #a1a1aa;
  --color-neutral-500: #71717a;
  --color-neutral-600: #52525b;
  --color-neutral-700: #3f3f46;
  --color-neutral-800: #27272a;
  --color-neutral-900: #18181b;
  --color-neutral-950: #09090b;
  --color-white: #ffffff;

  /* ========================================
     SEMANTIC - Estados
     ======================================== */
  --color-success: #10b981;
  --color-success-light: #d1fae5;
  --color-warning: #f59e0b;
  --color-warning-light: #fef3c7;
  --color-error: #ef4444;
  --color-error-light: #fee2e2;
  --color-info: #3b82f6;
  --color-info-light: #dbeafe;

  /* ========================================
     PRICING - Preços
     ======================================== */
  --color-free: #10b981;        /* Cursos gratuitos */
  --color-paid: #3b82f6;        /* Cursos pagos */
  --color-discount: #ef4444;    /* Desconto/Promoção */

  /* ========================================
     PLATFORMS - Badges de plataformas
     ======================================== */
  --color-udemy: #a435f0;
  --color-youtube: #ff0000;
  --color-hotmart: #f04e23;
  --color-eduzz: #00a8e8;
  --color-govbr: #1351b4;
  --color-coursera: #0056d2;
  --color-alura: #0056d2;

  /* ========================================
     RATINGS - Estrelas
     ======================================== */
  --color-star-filled: #f59e0b;
  --color-star-empty: #d4d4d8;

  /* ========================================
     BACKGROUNDS
     ======================================== */
  --bg-primary: var(--color-white);
  --bg-secondary: var(--color-neutral-50);
  --bg-tertiary: var(--color-neutral-100);
  --bg-inverse: var(--color-neutral-900);

  /* ========================================
     TEXT
     ======================================== */
  --text-primary: var(--color-neutral-900);
  --text-secondary: var(--color-neutral-600);
  --text-tertiary: var(--color-neutral-500);
  --text-inverse: var(--color-white);
  --text-muted: var(--color-neutral-400);

  /* ========================================
     DARK MODE
     ======================================== */
  --dark-bg-primary: #0f172a;
  --dark-bg-secondary: #1e293b;
  --dark-bg-tertiary: #334155;
  --dark-text-primary: #f1f5f9;
  --dark-text-secondary: #94a3b8;
  --dark-text-tertiary: #64748b;
}

/* Dark Mode Toggle */
[data-theme="dark"] {
  --bg-primary: var(--dark-bg-primary);
  --bg-secondary: var(--dark-bg-secondary);
  --bg-tertiary: var(--dark-bg-tertiary);
  --text-primary: var(--dark-text-primary);
  --text-secondary: var(--dark-text-secondary);
  --text-tertiary: var(--dark-text-tertiary);
}

/* System Preference */
@media (prefers-color-scheme: dark) {
  :root:not([data-theme="light"]) {
    --bg-primary: var(--dark-bg-primary);
    --bg-secondary: var(--dark-bg-secondary);
    --bg-tertiary: var(--dark-bg-tertiary);
    --text-primary: var(--dark-text-primary);
    --text-secondary: var(--dark-text-secondary);
    --text-tertiary: var(--dark-text-tertiary);
  }
}
```

### Tipografia

```css
:root {
  /* ========================================
     FONT FAMILIES
     ======================================== */
  --font-sans: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', 
               Roboto, 'Helvetica Neue', Arial, sans-serif;
  --font-heading: var(--font-sans);
  --font-mono: 'JetBrains Mono', 'Fira Code', 'SF Mono', Monaco, 
               Consolas, 'Liberation Mono', monospace;

  /* ========================================
     FONT SIZES - Scale 1.25 (Major Third)
     ======================================== */
  --text-xs: 0.75rem;      /* 12px */
  --text-sm: 0.875rem;     /* 14px */
  --text-base: 1rem;       /* 16px */
  --text-lg: 1.125rem;     /* 18px */
  --text-xl: 1.25rem;      /* 20px */
  --text-2xl: 1.5rem;      /* 24px */
  --text-3xl: 1.875rem;    /* 30px */
  --text-4xl: 2.25rem;     /* 36px */
  --text-5xl: 3rem;        /* 48px */
  --text-6xl: 3.75rem;     /* 60px */

  /* ========================================
     FONT WEIGHTS
     ======================================== */
  --font-light: 300;
  --font-normal: 400;
  --font-medium: 500;
  --font-semibold: 600;
  --font-bold: 700;
  --font-extrabold: 800;

  /* ========================================
     LINE HEIGHTS
     ======================================== */
  --leading-none: 1;
  --leading-tight: 1.25;
  --leading-snug: 1.375;
  --leading-normal: 1.5;
  --leading-relaxed: 1.625;
  --leading-loose: 2;

  /* ========================================
     LETTER SPACING
     ======================================== */
  --tracking-tighter: -0.05em;
  --tracking-tight: -0.025em;
  --tracking-normal: 0;
  --tracking-wide: 0.025em;
  --tracking-wider: 0.05em;
  --tracking-widest: 0.1em;
}
```

### Espaçamento (4px/8px Grid System)

```css
:root {
  /* ========================================
     SPACING SCALE - Base 4px
     ======================================== */
  --space-0: 0;
  --space-px: 1px;
  --space-0.5: 0.125rem;  /* 2px */
  --space-1: 0.25rem;     /* 4px */
  --space-1.5: 0.375rem;  /* 6px */
  --space-2: 0.5rem;      /* 8px */
  --space-2.5: 0.625rem;  /* 10px */
  --space-3: 0.75rem;     /* 12px */
  --space-3.5: 0.875rem;  /* 14px */
  --space-4: 1rem;        /* 16px */
  --space-5: 1.25rem;     /* 20px */
  --space-6: 1.5rem;      /* 24px */
  --space-7: 1.75rem;     /* 28px */
  --space-8: 2rem;        /* 32px */
  --space-10: 2.5rem;     /* 40px */
  --space-12: 3rem;       /* 48px */
  --space-14: 3.5rem;     /* 56px */
  --space-16: 4rem;       /* 64px */
  --space-20: 5rem;       /* 80px */
  --space-24: 6rem;       /* 96px */
  --space-32: 8rem;       /* 128px */

  /* ========================================
     CONTAINER WIDTHS
     ======================================== */
  --container-sm: 640px;
  --container-md: 768px;
  --container-lg: 1024px;
  --container-xl: 1280px;
  --container-2xl: 1536px;
  
  /* Max content width */
  --content-max: 1280px;
  --content-prose: 65ch;
}
```

### Border Radius

```css
:root {
  --radius-none: 0;
  --radius-sm: 0.125rem;   /* 2px */
  --radius-base: 0.25rem;  /* 4px */
  --radius-md: 0.375rem;   /* 6px */
  --radius-lg: 0.5rem;     /* 8px */
  --radius-xl: 0.75rem;    /* 12px */
  --radius-2xl: 1rem;      /* 16px */
  --radius-3xl: 1.5rem;    /* 24px */
  --radius-full: 9999px;
}
```

### Shadows

```css
:root {
  /* ========================================
     SHADOWS / ELEVATIONS
     ======================================== */
  --shadow-xs: 0 1px 2px 0 rgb(0 0 0 / 0.05);
  --shadow-sm: 0 1px 3px 0 rgb(0 0 0 / 0.1), 
               0 1px 2px -1px rgb(0 0 0 / 0.1);
  --shadow-md: 0 4px 6px -1px rgb(0 0 0 / 0.1), 
               0 2px 4px -2px rgb(0 0 0 / 0.1);
  --shadow-lg: 0 10px 15px -3px rgb(0 0 0 / 0.1), 
               0 4px 6px -4px rgb(0 0 0 / 0.1);
  --shadow-xl: 0 20px 25px -5px rgb(0 0 0 / 0.1), 
               0 8px 10px -6px rgb(0 0 0 / 0.1);
  --shadow-2xl: 0 25px 50px -12px rgb(0 0 0 / 0.25);
  --shadow-inner: inset 0 2px 4px 0 rgb(0 0 0 / 0.05);

  /* Card shadows */
  --shadow-card: var(--shadow-sm);
  --shadow-card-hover: var(--shadow-lg);

  /* Focus ring */
  --ring-color: rgb(16 185 129 / 0.5);
  --shadow-focus: 0 0 0 2px var(--bg-primary), 0 0 0 4px var(--ring-color);
}
```

### Z-Index Scale

```css
:root {
  --z-0: 0;
  --z-10: 10;
  --z-20: 20;
  --z-30: 30;
  --z-40: 40;
  --z-50: 50;
  
  /* Semantic Z-Index */
  --z-dropdown: 1000;
  --z-sticky: 1020;
  --z-fixed: 1030;
  --z-modal-backdrop: 1040;
  --z-modal: 1050;
  --z-popover: 1060;
  --z-tooltip: 1070;
  --z-toast: 1080;
}
```

---

## 🧩 COMPONENTES BASE (REFERÊNCIA)

Os componentes devem seguir o design system. Aqui estão os principais componentes do projeto:

### Course Card

O card de curso é o componente mais importante. Deve conter:
- Imagem (aspect-ratio 16/9)
- Badge da plataforma
- Badge "Grátis" (se aplicável)
- Título (máximo 2 linhas)
- Instrutor
- Rating com estrelas
- Preço
- Schema.org markup (itemScope, itemType="Course")

### Platform Badge

Badges coloridos para cada plataforma:
- Udemy: roxo (#a435f0)
- YouTube: vermelho (#ff0000)
- Hotmart: laranja (#f04e23)
- Gov.br: azul (#1351b4)
- Etc.

### Star Rating

Componente de estrelas que mostra:
- Estrelas preenchidas (amarelo)
- Nota numérica
- Contador de avaliações

### Price Tag

Exibe preço formatado em BRL:
- "Grátis" para cursos gratuitos (verde)
- Preço atual + preço original riscado (se houver desconto)

### Button

Variantes:
- Primary (verde)
- Secondary (azul)
- Outline
- Ghost
- Danger
- Link

Tamanhos: sm, md, lg, xl, icon

---

## 💻 STACK TECNOLÓGICO

### Backend (CMS)
| Tecnologia | Versão | Justificativa |
|------------|--------|---------------|
| **Strapi** | v5+ | Headless CMS, API-first, admin pronto |
| **PostgreSQL** | 16+ | Full-text search nativo, robusto |
| **Node.js** | 20 LTS | Runtime do Strapi |

### Frontend
| Tecnologia | Versão | Justificativa |
|------------|--------|---------------|
| **Next.js** | 14+ | App Router, SSR/SSG, SEO |
| **React** | 18+ | Biblioteca UI |
| **TypeScript** | 5+ | Type safety |
| **Tailwind CSS** | 3.4+ | Utility-first |

### Bibliotecas Essenciais
| Biblioteca | Uso |
|------------|-----|
| `lucide-react` | Ícones |
| `class-variance-authority` | Variants |
| `clsx` + `tailwind-merge` | Classes |
| `@radix-ui/*` | Primitivos acessíveis |
| `react-hook-form` + `zod` | Formulários |
| `qs` | Query strings |

### Infraestrutura
| Serviço | Uso |
|---------|-----|
| **Coolify** | Deploy |
| **Cloudflare** | CDN, SSL |
| **Redis** | Cache (futuro) |

---

## 🤖 AGENTES ESPECIALIZADOS

### 1. Frontend Developer Agent (Claude Code)

**Responsabilidade:** Desenvolver componentes e páginas Next.js

**Contexto Base:**
```
Você é um desenvolvedor frontend sênior especializado em Next.js 14+ (App Router), React 18, TypeScript e Tailwind CSS, trabalhando no projeto habilite.me - um agregador de cursos para brasileiros.

STACK:
- Next.js 14+ (App Router)
- React 18+ (Server Components por padrão)
- TypeScript 5+ (strict mode)
- Tailwind CSS 3.4+

PRINCÍPIOS OBRIGATÓRIOS:
1. Server Components por padrão, Client Components apenas quando necessário
2. TypeScript strict mode sempre
3. Mobile-first, responsivo
4. Acessibilidade WCAG 2.1 AA
5. Performance (Core Web Vitals: LCP < 2.5s, FID < 100ms, CLS < 0.1)
6. SEO otimizado (meta tags, JSON-LD, sitemap)
7. Usar design system definido (cores, tipografia, espaçamento)

DESIGN SYSTEM:
[Incluir variáveis CSS do design system]

PADRÕES DE COMPONENTES:
- Componentes em /components organizados por domínio
- UI primitivos em /components/ui
- Props tipadas com interface
- Usar cn() para merge de classes
```

**Especialidades:**
- Pages e Layouts (App Router)
- Server Components
- Data fetching (RSC)
- SEO e JSON-LD
- Responsividade
- Acessibilidade

---

### 2. Strapi Developer Agent (Claude)

**Responsabilidade:** Configurar e customizar o Strapi CMS

**Contexto Base:**
```
Você é um desenvolvedor backend especializado em Strapi v5, trabalhando no projeto habilite.me.

STACK:
- Strapi v5
- PostgreSQL 16+
- Node.js 20 LTS

COLLECTIONS DO PROJETO:
1. Cursos: título, slug, descrição, preço, categoria, plataforma, status, SEO
2. Categorias: nome, slug, descrição, categoria_pai
3. Reviews: curso, usuario, nota, comentario, aprovado
4. Blog Posts: título, slug, conteúdo, cursos_relacionados
5. Submissions: dados do curso, contato, status

PRINCÍPIOS:
- Content-Types bem estruturados
- Lifecycle hooks para automação (SEO, slugs)
- Validações robustas
- Permissões granulares
- API otimizada (populate seletivo)
```

**Especialidades:**
- Content-Types
- Lifecycle hooks
- Custom controllers
- Permissions

---

### 3. SEO Specialist Agent (Claude)

**Responsabilidade:** Otimizar SEO técnico e on-page

**Contexto Base:**
```
Você é especialista em SEO técnico e on-page para Next.js.

PILARES SEO:

1. TECHNICAL SEO:
   - Sitemap XML dinâmico
   - Robots.txt otimizado
   - Canonical URLs
   - Performance (Core Web Vitals)
   - Mobile-first indexing

2. ON-PAGE SEO:
   - Title tags (50-60 chars, keyword no início)
   - Meta descriptions (150-155 chars, CTA)
   - Header hierarchy (H1 único)
   - URL semânticas
   - Internal linking

3. SCHEMA.ORG (JSON-LD):
   - Course (páginas de curso)
   - ItemList (listagens)
   - AggregateRating (reviews)
   - BreadcrumbList
   - BlogPosting (posts)

4. NEXT.JS ESPECÍFICO:
   - generateMetadata()
   - generateStaticParams()
   - sitemap.ts
   - robots.ts
```

**Especialidades:**
- Meta tags
- JSON-LD schemas
- Sitemap
- Performance SEO

---

### 4. UI/UX Designer Agent (Claude)

**Responsabilidade:** Criar interfaces otimizadas

**Contexto Base:**
```
Você é designer UI/UX especializado em sites de conteúdo e conversão.

DESIGN SYSTEM HABILITE.ME:
[Incluir todas as variáveis CSS]

PRINCÍPIOS:
- Clareza > Complexidade
- Hierarquia visual clara
- Espaçamento generoso (8px grid)
- Tipografia legível
- Contraste adequado (WCAG AA: 4.5:1)
- Mobile-first
- Microinterações sutis

ACESSIBILIDADE WCAG 2.1 AA:
- Contraste mínimo 4.5:1 (texto normal)
- Focus states visíveis
- Navegação por teclado
- Screen reader friendly
- ARIA labels quando necessário

RESPONSIVE BREAKPOINTS:
- sm: 640px
- md: 768px
- lg: 1024px
- xl: 1280px
- 2xl: 1536px
```

---

### 5. Performance Optimizer Agent (Claude)

**Responsabilidade:** Otimizar Core Web Vitals

**Contexto Base:**
```
Você é especialista em performance web para Next.js.

MÉTRICAS TARGET:
- LCP: < 2.5s
- FID: < 100ms
- CLS: < 0.1
- PageSpeed: 90+ mobile

TÉCNICAS NEXT.JS:
- Server Components
- next/image
- next/font
- ISR
- Streaming com Suspense

OTIMIZAÇÕES:
- Code splitting
- Dynamic imports
- Lazy loading
- Cache headers
```

---

### 6. Content Generator Agent (Claude)

**Responsabilidade:** Gerar conteúdo para blog

**Contexto Base:**
```
Você é redator especializado em educação e cursos para brasileiros.

PÚBLICO-ALVO:
- Brasileiros buscando qualificação
- Profissionais em transição de carreira
- Estudantes

TOM:
- Acessível e encorajador
- Informativo e prático
- Foco em resultados

TIPOS DE CONTEÚDO:
- Reviews de cursos
- Guias "Como aprender X"
- Listas "Melhores cursos de X"
- Notícias do setor

SEO:
- Keyword density: 0.5-1%
- Links internos: 3-5
- Meta title: 50-60 chars
- Meta description: 150-155 chars
```

---

## 📝 PROMPTS BASE

### Prompt: Criar Página Next.js

```markdown
TAREFA: Criar página '[NOME]'

ROTA: /[rota]
TIPO: [SSG | SSR | ISR]

DADOS STRAPI:
- Collection: [nome]
- Campos: [listar]
- Filtros: [se houver]

LAYOUT:
[Descrever estrutura]

COMPONENTES:
- [Listar componentes]

SEO:
- Title: [título]
- Description: [descrição]
- Schema.org: [tipo]

REQUISITOS:
- [ ] Server Component
- [ ] generateMetadata()
- [ ] JSON-LD
- [ ] Loading state
- [ ] Error handling
- [ ] Responsivo
- [ ] Acessível

ENTREGA:
- page.tsx
- loading.tsx
- error.tsx
```

---

### Prompt: Criar Componente

```markdown
TAREFA: Criar componente '[NOME]'

TIPO: [Server | Client]

PROPS:
```typescript
interface Props {
  prop1: tipo;
  prop2?: tipo;
}
```

VARIANTES: [se houver]

ESTADOS:
- Default
- Hover
- Focus
- Disabled
- Loading

ACESSIBILIDADE:
- [ ] Role
- [ ] ARIA labels
- [ ] Keyboard nav
- [ ] Focus visible

ENTREGA:
- Componente TSX
- Exemplo de uso
```

---

### Prompt: Implementar SEO

```markdown
TAREFA: SEO para [página]

META TAGS:
- title: [max 60 chars]
- description: [max 155 chars]
- canonical: [URL]

OPEN GRAPH:
- og:title
- og:description
- og:image
- og:url

JSON-LD:
- @type: [Course | ItemList | BlogPosting]
- Campos obrigatórios

ENTREGA:
- generateMetadata()
- JSON-LD component
```

---

## 🔄 WORKFLOWS DE DESENVOLVIMENTO

### Workflow: Nova Página

```
1. Definir requisitos (15min)
2. Verificar/criar collection Strapi (30min)
3. Criar tipos TypeScript (15min)
4. Implementar data fetching (30min)
5. Criar/reutilizar componentes (1-2h)
6. Montar página (30min)
7. Implementar SEO (30min)
8. Testar responsividade (20min)
9. Testar acessibilidade (20min)
10. Otimizar performance (30min)
11. Code review (20min)
12. Deploy (10min)

TEMPO TOTAL: ~5-6 horas (página complexa)
```

### Workflow: Novo Componente

```
1. Definir propósito e props (10min)
2. Criar estrutura TSX (20min)
3. Estilizar com Tailwind (30min)
4. Adicionar interatividade (20min)
5. Implementar acessibilidade (15min)
6. Testar variantes (15min)
7. Documentar (10min)

TEMPO TOTAL: ~2 horas
```

---

## 📐 PADRÕES DE CÓDIGO

### TypeScript

```typescript
// ✅ BOM: Tipos explícitos
interface Course {
  id: number;
  titulo: string;
  slug: string;
  preco: number | null;
  plataforma: Platform;
}

type Platform = 'udemy' | 'youtube' | 'hotmart' | 'govbr';

// ❌ RUIM: any
const course: any = { ... };
```

### React/Next.js

```tsx
// ✅ BOM: Server Component
import { Suspense } from 'react';

export default function Page() {
  return (
    <Suspense fallback={<Skeleton />}>
      <CourseGrid />
    </Suspense>
  );
}

// ❌ RUIM: Client Component desnecessário
'use client';
import { useState, useEffect } from 'react';

export default function Page() {
  const [data, setData] = useState([]);
  useEffect(() => { fetch(...) }, []);
  return <div>{...}</div>;
}
```

### Tailwind

```tsx
// ✅ BOM: Classes organizadas
<button className={cn(
  "inline-flex items-center justify-center",
  "h-10 px-4 text-sm font-medium",
  "bg-primary-600 text-white rounded-lg",
  "hover:bg-primary-700 transition-colors",
  disabled && "opacity-50 cursor-not-allowed"
)}>

// ❌ RUIM: Inline styles
<button style={{ backgroundColor: '#10b981' }}>
```

### Estrutura de Arquivos

```
components/
├── ui/              # Primitivos
│   ├── button.tsx
│   ├── card.tsx
│   └── index.ts
├── courses/         # Domínio: cursos
│   ├── course-card.tsx
│   └── course-grid.tsx
├── blog/            # Domínio: blog
│   └── post-card.tsx
└── layout/          # Layout global
    ├── header.tsx
    └── footer.tsx
```

---

## ✅ TESTES E VALIDAÇÃO

### Checklist - Componente

- [ ] TypeScript sem erros
- [ ] Props tipadas
- [ ] Acessível (ARIA, keyboard)
- [ ] Responsivo
- [ ] Design system aplicado
- [ ] Estados cobertos

### Checklist - Página

- [ ] Server Component
- [ ] generateMetadata()
- [ ] JSON-LD válido
- [ ] Loading state
- [ ] Error handling
- [ ] Responsivo
- [ ] Acessível
- [ ] Performance (Lighthouse 90+)

### Checklist - SEO

- [ ] Title tag (50-60 chars)
- [ ] Meta description (150-155 chars)
- [ ] H1 único
- [ ] Canonical URL
- [ ] OG tags
- [ ] JSON-LD válido
- [ ] Sitemap atualizado

### Ferramentas

| Ferramenta | Uso |
|------------|-----|
| `tsc --noEmit` | TypeScript |
| Lighthouse | Performance/SEO |
| axe DevTools | Acessibilidade |
| Rich Results Test | Schema.org |

---

## 📚 RECURSOS

- [Next.js Docs](https://nextjs.org/docs)
- [Tailwind CSS](https://tailwindcss.com/docs)
- [Strapi Docs](https://docs.strapi.io)
- [Schema.org](https://schema.org)
- [WCAG 2.1](https://www.w3.org/WAI/WCAG21/quickref)
- [web.dev](https://web.dev)

---

**Versão:** 1.0  
**Última atualização:** Janeiro 2025  
**Maintainer:** Equipe habilite.me
