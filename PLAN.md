# habilite.me: Plano de Implementação Técnica v1.0

> **Agregador de Cursos para Brasileiros** - Plataforma de descoberta de cursos gratuitos e pagos com foco em SEO, afiliação e divulgação em redes sociais.

---

## 1. Visão Geral da Arquitetura

O sistema opera em uma arquitetura **headless CMS + SSG/SSR**, com Strapi gerenciando o conteúdo e Next.js renderizando o frontend otimizado para SEO.

### 1.1 Filosofia: Começar Simples, Escalar com Demanda

```
┌─────────────────────────────────────────────────────────────┐
│  FASE 1: MVP (Validação - Semanas 1-3)                      │
│  • ~30-50 cursos cadastrados manualmente                    │
│  • Blog com 5-10 posts iniciais                             │
│  • SEO básico funcionando                                   │
│  • Foco: Validar tração orgânica                            │
├─────────────────────────────────────────────────────────────┤
│  FASE 2: Expansão (Semanas 4-6)                             │
│  • Sistema de reviews                                       │
│  • Página "Divulgue seu Curso"                              │
│  • ~100-200 cursos                                          │
│  • Foco: Engajamento e submissões                           │
├─────────────────────────────────────────────────────────────┤
│  FASE 3: Monetização (Semanas 7-8)                          │
│  • Links de afiliação otimizados                            │
│  • AdSense implementado                                     │
│  • Analytics completo                                       │
│  • Foco: Gerar receita                                      │
├─────────────────────────────────────────────────────────────┤
│  FASE 4: Automação (Futuro)                                 │
│  • Agentes de scraping/API                                  │
│  • Fila de aprovação automática                             │
│  • Foco: Escalar catálogo                                   │
└─────────────────────────────────────────────────────────────┘
```

### 1.2 Tech Stack

| Camada | Tecnologia | Versão | Justificativa |
|--------|------------|--------|---------------|
| **CMS** | Strapi | v5+ | Headless, admin pronto, API-first |
| **Database** | PostgreSQL | 16+ | Full-text search, robusto |
| **Frontend** | Next.js | 14+ | App Router, SSR/SSG, SEO |
| **Styling** | Tailwind CSS | 3.4+ | Utility-first, produtivo |
| **Language** | TypeScript | 5+ | Type safety |
| **Deploy** | Coolify | - | Self-hosted, Docker |
| **CDN** | Cloudflare | Free | Cache, SSL, proteção |

### 1.3 Estimativa de Custos (MVP)

| Serviço | Custo mensal |
|---------|--------------|
| VPS (Coolify) | R$ 0 (já pago) |
| Domínio .me | ~R$ 7/mês (anual) |
| Cloudflare | R$ 0 |
| **TOTAL** | **~R$ 7/mês** |

### 1.4 Diagrama de Arquitetura

```
┌─────────────────────────────────────────────────────────────┐
│                      CLOUDFLARE                              │
│                   (CDN + SSL + Cache)                        │
└─────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│                      COOLIFY SERVER                          │
│                                                              │
│  ┌───────────────────┐        ┌───────────────────┐         │
│  │     NEXT.JS       │        │      STRAPI       │         │
│  │    (Frontend)     │◄──────►│      (CMS)        │         │
│  │                   │        │                   │         │
│  │  • SSR/SSG/ISR    │        │  • Admin Panel    │         │
│  │  • API Routes     │        │  • REST API       │         │
│  │                   │        │  • Auth           │         │
│  │  Port: 3000       │        │  Port: 1337       │         │
│  └───────────────────┘        └───────────────────┘         │
│           │                            │                     │
│           └────────────┬───────────────┘                     │
│                        │                                     │
│                        ▼                                     │
│           ┌───────────────────────┐                          │
│           │     POSTGRESQL        │                          │
│           │     (Database)        │                          │
│           │                       │                          │
│           │  Port: 5432           │                          │
│           └───────────────────────┘                          │
│                                                              │
└──────────────────────────────────────────────────────────────┘
```

---

## 2. Estrutura do Projeto

### 2.1 Estrutura de Pastas

```
habilite.me/
├── apps/
│   ├── web/                          # Next.js Frontend
│   │   ├── app/
│   │   │   ├── (marketing)/          # Páginas públicas
│   │   │   │   ├── layout.tsx
│   │   │   │   ├── page.tsx          # Home
│   │   │   │   │
│   │   │   │   ├── cursos/
│   │   │   │   │   ├── page.tsx      # Lista de cursos
│   │   │   │   │   └── [categoria]/
│   │   │   │   │       └── page.tsx  # Por categoria
│   │   │   │   │
│   │   │   │   ├── curso/
│   │   │   │   │   └── [slug]/
│   │   │   │   │       └── page.tsx  # Detalhe do curso
│   │   │   │   │
│   │   │   │   ├── blog/
│   │   │   │   │   ├── page.tsx      # Lista de posts
│   │   │   │   │   └── [slug]/
│   │   │   │   │       └── page.tsx  # Post individual
│   │   │   │   │
│   │   │   │   ├── categorias/
│   │   │   │   │   └── page.tsx      # Lista categorias
│   │   │   │   │
│   │   │   │   ├── sobre/
│   │   │   │   │   └── page.tsx
│   │   │   │   │
│   │   │   │   ├── contato/
│   │   │   │   │   └── page.tsx
│   │   │   │   │
│   │   │   │   └── divulgue-seu-curso/
│   │   │   │       └── page.tsx
│   │   │   │
│   │   │   ├── api/
│   │   │   │   ├── revalidate/
│   │   │   │   │   └── route.ts      # ISR webhook
│   │   │   │   ├── reviews/
│   │   │   │   │   └── route.ts      # Submit review
│   │   │   │   └── submission/
│   │   │   │       └── route.ts      # Course submission
│   │   │   │
│   │   │   ├── layout.tsx            # Root layout
│   │   │   ├── not-found.tsx
│   │   │   ├── error.tsx
│   │   │   ├── loading.tsx
│   │   │   ├── robots.ts
│   │   │   ├── sitemap.ts
│   │   │   └── globals.css
│   │   │
│   │   ├── components/
│   │   │   ├── ui/                   # Primitivos
│   │   │   │   ├── button.tsx
│   │   │   │   ├── card.tsx
│   │   │   │   ├── input.tsx
│   │   │   │   ├── badge.tsx
│   │   │   │   ├── star-rating.tsx
│   │   │   │   ├── price-tag.tsx
│   │   │   │   ├── platform-badge.tsx
│   │   │   │   ├── skeleton.tsx
│   │   │   │   └── index.ts
│   │   │   │
│   │   │   ├── courses/              # Cursos
│   │   │   │   ├── course-card.tsx
│   │   │   │   ├── course-grid.tsx
│   │   │   │   ├── course-filters.tsx
│   │   │   │   ├── course-search.tsx
│   │   │   │   └── related-courses.tsx
│   │   │   │
│   │   │   ├── blog/                 # Blog
│   │   │   │   ├── post-card.tsx
│   │   │   │   └── post-content.tsx
│   │   │   │
│   │   │   ├── reviews/              # Reviews
│   │   │   │   ├── review-list.tsx
│   │   │   │   ├── review-form.tsx
│   │   │   │   └── review-summary.tsx
│   │   │   │
│   │   │   ├── forms/                # Formulários
│   │   │   │   ├── contact-form.tsx
│   │   │   │   ├── submission-form.tsx
│   │   │   │   └── newsletter-form.tsx
│   │   │   │
│   │   │   ├── layout/               # Layout
│   │   │   │   ├── header.tsx
│   │   │   │   ├── footer.tsx
│   │   │   │   ├── mobile-menu.tsx
│   │   │   │   └── breadcrumbs.tsx
│   │   │   │
│   │   │   └── seo/                  # SEO
│   │   │       └── json-ld.tsx
│   │   │
│   │   ├── lib/
│   │   │   ├── strapi/
│   │   │   │   ├── client.ts         # API client
│   │   │   │   ├── queries.ts        # Queries
│   │   │   │   └── types.ts          # Types
│   │   │   │
│   │   │   └── utils/
│   │   │       ├── cn.ts             # classnames
│   │   │       ├── format.ts         # Formatters
│   │   │       └── seo.ts            # SEO helpers
│   │   │
│   │   ├── types/
│   │   │   ├── course.ts
│   │   │   ├── category.ts
│   │   │   ├── review.ts
│   │   │   ├── blog.ts
│   │   │   └── index.ts
│   │   │
│   │   ├── public/
│   │   │   ├── images/
│   │   │   └── icons/
│   │   │
│   │   ├── next.config.js
│   │   ├── tailwind.config.js
│   │   ├── tsconfig.json
│   │   └── package.json
│   │
│   └── cms/                          # Strapi
│       ├── config/
│       │   ├── database.ts
│       │   ├── server.ts
│       │   └── plugins.ts
│       │
│       ├── src/
│       │   ├── api/
│       │   │   ├── curso/
│       │   │   ├── categoria/
│       │   │   ├── review/
│       │   │   ├── blog-post/
│       │   │   └── submission/
│       │   │
│       │   └── components/
│       │       └── seo/
│       │
│       └── package.json
│
├── docker/
│   ├── docker-compose.yml
│   └── docker-compose.dev.yml
│
├── docs/
│   ├── AGENTS.md
│   └── PLAN.md
│
├── .env.example
├── .gitignore
└── README.md
```

---

## 3. Schema do Banco de Dados (Strapi)

### 3.1 Collection: Cursos

```json
{
  "kind": "collectionType",
  "collectionName": "cursos",
  "info": {
    "singularName": "curso",
    "pluralName": "cursos",
    "displayName": "Curso"
  },
  "options": {
    "draftAndPublish": true
  },
  "attributes": {
    "titulo": {
      "type": "string",
      "required": true,
      "maxLength": 200
    },
    "slug": {
      "type": "uid",
      "targetField": "titulo",
      "required": true
    },
    "descricao": {
      "type": "richtext"
    },
    "descricao_curta": {
      "type": "text",
      "maxLength": 300
    },
    "url_original": {
      "type": "string",
      "required": true
    },
    "url_afiliado": {
      "type": "string"
    },
    "plataforma": {
      "type": "enumeration",
      "enum": ["udemy", "youtube", "hotmart", "eduzz", "govbr", "coursera", "alura", "outros"],
      "required": true
    },
    "tipo": {
      "type": "enumeration",
      "enum": ["gratuito", "pago", "freemium"],
      "default": "pago"
    },
    "preco": {
      "type": "decimal",
      "min": 0
    },
    "preco_original": {
      "type": "decimal",
      "min": 0
    },
    "instrutor": {
      "type": "string",
      "maxLength": 200
    },
    "duracao_horas": {
      "type": "decimal",
      "min": 0
    },
    "num_aulas": {
      "type": "integer",
      "min": 0
    },
    "nivel": {
      "type": "enumeration",
      "enum": ["iniciante", "intermediario", "avancado", "todos"],
      "default": "todos"
    },
    "idioma": {
      "type": "string",
      "default": "pt-BR"
    },
    "nota": {
      "type": "decimal",
      "min": 0,
      "max": 5
    },
    "num_avaliacoes": {
      "type": "integer",
      "min": 0,
      "default": 0
    },
    "tags": {
      "type": "json"
    },
    "status": {
      "type": "enumeration",
      "enum": ["pendente", "aprovado", "rejeitado"],
      "default": "pendente"
    },
    "destaque": {
      "type": "boolean",
      "default": false
    },
    "categoria": {
      "type": "relation",
      "relation": "manyToOne",
      "target": "api::categoria.categoria",
      "inversedBy": "cursos"
    },
    "imagem": {
      "type": "media",
      "allowedTypes": ["images"]
    },
    "reviews": {
      "type": "relation",
      "relation": "oneToMany",
      "target": "api::review.review",
      "mappedBy": "curso"
    },
    "seo": {
      "type": "component",
      "repeatable": false,
      "component": "seo.seo"
    }
  }
}
```

### 3.2 Collection: Categorias

```json
{
  "kind": "collectionType",
  "collectionName": "categorias",
  "info": {
    "singularName": "categoria",
    "pluralName": "categorias",
    "displayName": "Categoria"
  },
  "attributes": {
    "nome": {
      "type": "string",
      "required": true,
      "maxLength": 100
    },
    "slug": {
      "type": "uid",
      "targetField": "nome",
      "required": true
    },
    "descricao": {
      "type": "text",
      "maxLength": 500
    },
    "icone": {
      "type": "string",
      "maxLength": 50
    },
    "cor": {
      "type": "string"
    },
    "ordem": {
      "type": "integer",
      "default": 0
    },
    "ativa": {
      "type": "boolean",
      "default": true
    },
    "categoria_pai": {
      "type": "relation",
      "relation": "manyToOne",
      "target": "api::categoria.categoria"
    },
    "cursos": {
      "type": "relation",
      "relation": "oneToMany",
      "target": "api::curso.curso",
      "mappedBy": "categoria"
    },
    "imagem": {
      "type": "media",
      "allowedTypes": ["images"]
    },
    "seo": {
      "type": "component",
      "repeatable": false,
      "component": "seo.seo"
    }
  }
}
```

### 3.3 Collection: Reviews

```json
{
  "kind": "collectionType",
  "collectionName": "reviews",
  "info": {
    "singularName": "review",
    "pluralName": "reviews",
    "displayName": "Review"
  },
  "attributes": {
    "nome": {
      "type": "string",
      "required": true,
      "maxLength": 100
    },
    "email": {
      "type": "email",
      "required": true,
      "private": true
    },
    "nota": {
      "type": "integer",
      "required": true,
      "min": 1,
      "max": 5
    },
    "titulo": {
      "type": "string",
      "maxLength": 200
    },
    "comentario": {
      "type": "text",
      "required": true,
      "maxLength": 2000
    },
    "aprovado": {
      "type": "boolean",
      "default": false
    },
    "curso": {
      "type": "relation",
      "relation": "manyToOne",
      "target": "api::curso.curso",
      "inversedBy": "reviews"
    }
  }
}
```

### 3.4 Collection: Blog Posts

```json
{
  "kind": "collectionType",
  "collectionName": "blog_posts",
  "info": {
    "singularName": "blog-post",
    "pluralName": "blog-posts",
    "displayName": "Blog Post"
  },
  "options": {
    "draftAndPublish": true
  },
  "attributes": {
    "titulo": {
      "type": "string",
      "required": true,
      "maxLength": 200
    },
    "slug": {
      "type": "uid",
      "targetField": "titulo",
      "required": true
    },
    "resumo": {
      "type": "text",
      "maxLength": 300
    },
    "conteudo": {
      "type": "richtext",
      "required": true
    },
    "imagem_capa": {
      "type": "media",
      "allowedTypes": ["images"]
    },
    "autor": {
      "type": "string",
      "default": "Equipe habilite.me"
    },
    "categoria": {
      "type": "enumeration",
      "enum": ["noticias", "dicas", "tutoriais", "carreira", "concursos", "tecnologia"]
    },
    "tags": {
      "type": "json"
    },
    "tempo_leitura": {
      "type": "integer"
    },
    "destaque": {
      "type": "boolean",
      "default": false
    },
    "cursos_relacionados": {
      "type": "relation",
      "relation": "manyToMany",
      "target": "api::curso.curso"
    },
    "seo": {
      "type": "component",
      "repeatable": false,
      "component": "seo.seo"
    }
  }
}
```

### 3.5 Collection: Submissions

```json
{
  "kind": "collectionType",
  "collectionName": "submissions",
  "info": {
    "singularName": "submission",
    "pluralName": "submissions",
    "displayName": "Submission"
  },
  "attributes": {
    "nome_contato": {
      "type": "string",
      "required": true
    },
    "email": {
      "type": "email",
      "required": true
    },
    "telefone": {
      "type": "string"
    },
    "nome_curso": {
      "type": "string",
      "required": true
    },
    "url_curso": {
      "type": "string",
      "required": true
    },
    "plataforma": {
      "type": "string",
      "required": true
    },
    "descricao": {
      "type": "text"
    },
    "tipo_parceria": {
      "type": "enumeration",
      "enum": ["afiliacao", "divulgacao", "troca", "outro"]
    },
    "mensagem": {
      "type": "text"
    },
    "status": {
      "type": "enumeration",
      "enum": ["novo", "em_analise", "aprovado", "rejeitado"],
      "default": "novo"
    }
  }
}
```

### 3.6 Component: SEO

```json
{
  "collectionName": "components_seo_seos",
  "info": {
    "displayName": "SEO",
    "icon": "search"
  },
  "attributes": {
    "titulo": {
      "type": "string",
      "maxLength": 60
    },
    "descricao": {
      "type": "text",
      "maxLength": 160
    },
    "imagem_og": {
      "type": "media",
      "allowedTypes": ["images"]
    },
    "keywords": {
      "type": "string",
      "maxLength": 200
    },
    "canonical_url": {
      "type": "string"
    },
    "no_index": {
      "type": "boolean",
      "default": false
    }
  }
}
```

---

## 4. Páginas do Frontend

### 4.1 Home (/)

**Objetivo:** Landing page que apresenta o site e seus principais cursos.

**Seções:**
1. Hero com busca
2. Cursos em destaque (6-8 cards)
3. Categorias populares
4. Como funciona (3 passos)
5. Posts recentes do blog (3 cards)
6. CTA para divulgar curso
7. Newsletter

**SEO:**
- Title: "habilite.me - Cursos Online Gratuitos e Pagos para Brasileiros"
- Description: "Encontre os melhores cursos online gratuitos e pagos. Programação, marketing, design, idiomas e muito mais. Compare plataformas e comece a estudar hoje!"
- Schema: WebSite, Organization

---

### 4.2 Listagem de Cursos (/cursos)

**Objetivo:** Página de busca e listagem de todos os cursos.

**Features:**
- Grid de cards (12 por página)
- Filtros: categoria, tipo (grátis/pago), plataforma, nível
- Busca por texto
- Ordenação (relevância, preço, avaliação, recentes)
- Paginação

**SEO:**
- Title: "Cursos Online Gratuitos e Pagos | habilite.me"
- Description: "Encontre cursos de programação, marketing, design, idiomas e muito mais. Compare preços e avaliações das melhores plataformas."
- Schema: ItemList

---

### 4.3 Cursos por Categoria (/cursos/[categoria])

**Objetivo:** Listagem filtrada por categoria.

**Features:**
- Mesmo layout de /cursos
- Descrição da categoria
- Filtros pré-aplicados
- Subcategorias (se houver)

**SEO:**
- Title dinâmico: "Cursos de {Categoria} Online | habilite.me"
- Description dinâmico baseado na categoria
- Schema: ItemList

---

### 4.4 Página do Curso (/curso/[slug])

**Objetivo:** Página de detalhes do curso com CTA para plataforma.

**Seções:**
1. Hero com imagem, título, rating, preço
2. Botão CTA (link afiliado)
3. Sobre o curso (descrição completa)
4. Informações (duração, nível, idioma, aulas)
5. Reviews dos usuários
6. Formulário de review
7. Cursos relacionados

**SEO:**
- Title: "{Nome do Curso} | habilite.me"
- Description: descrição_curta do curso
- Schema: Course, AggregateRating

---

### 4.5 Blog (/blog)

**Objetivo:** Listagem de posts do blog.

**Features:**
- Grid de cards
- Filtro por categoria
- Posts em destaque
- Paginação

**SEO:**
- Title: "Blog | habilite.me - Dicas de Cursos e Carreira"
- Schema: Blog

---

### 4.6 Post do Blog (/blog/[slug])

**Objetivo:** Página do artigo completo.

**Seções:**
1. Header com título, autor, data
2. Imagem de capa
3. Conteúdo do post
4. Cursos relacionados
5. Posts relacionados
6. Compartilhamento social

**SEO:**
- Title: "{Título do Post} | Blog habilite.me"
- Schema: BlogPosting

---

### 4.7 Categorias (/categorias)

**Objetivo:** Lista todas as categorias disponíveis.

**Features:**
- Grid de cards de categorias
- Contador de cursos por categoria
- Descrição breve

---

### 4.8 Sobre (/sobre)

**Objetivo:** Apresentar o projeto e equipe.

**Seções:**
1. Missão do habilite.me
2. Como funciona
3. Quem somos
4. Contato

---

### 4.9 Contato (/contato)

**Objetivo:** Formulário de contato geral.

**Features:**
- Formulário: nome, email, assunto, mensagem
- Informações de contato
- FAQ

---

### 4.10 Divulgue seu Curso (/divulgue-seu-curso)

**Objetivo:** Formulário para produtores de conteúdo.

**Features:**
- Benefícios de divulgar no habilite.me
- Formulário de submissão
- Tipos de parceria
- FAQ para produtores

---

## 5. Componentes Principais

### 5.1 Layout Components

| Componente | Descrição |
|------------|-----------|
| `Header` | Navegação principal, logo, busca, menu mobile |
| `Footer` | Links, redes sociais, newsletter, copyright |
| `MobileMenu` | Menu lateral para mobile |
| `Breadcrumbs` | Navegação hierárquica |

### 5.2 Course Components

| Componente | Descrição |
|------------|-----------|
| `CourseCard` | Card com imagem, título, preço, rating |
| `CourseGrid` | Grid responsivo de CourseCards |
| `CourseFilters` | Filtros (categoria, tipo, plataforma) |
| `CourseSearch` | Input de busca |
| `RelatedCourses` | Lista de cursos relacionados |

### 5.3 UI Components

| Componente | Descrição |
|------------|-----------|
| `Button` | Botão com variants |
| `Card` | Container base |
| `Badge` | Label/tag |
| `Input` | Campo de texto |
| `Select` | Dropdown |
| `StarRating` | Rating com estrelas |
| `PriceTag` | Exibição de preço |
| `PlatformBadge` | Badge da plataforma |
| `Skeleton` | Loading placeholder |

### 5.4 Review Components

| Componente | Descrição |
|------------|-----------|
| `ReviewList` | Lista de reviews |
| `ReviewForm` | Formulário de review |
| `ReviewSummary` | Resumo (média, distribuição) |

### 5.5 Blog Components

| Componente | Descrição |
|------------|-----------|
| `PostCard` | Card do post |
| `PostContent` | Renderização do conteúdo |

### 5.6 Form Components

| Componente | Descrição |
|------------|-----------|
| `ContactForm` | Formulário de contato |
| `SubmissionForm` | Formulário de submissão de curso |
| `NewsletterForm` | Inscrição newsletter |

---

## 6. SEO Strategy

### 6.1 URLs Structure

```
/                           # Home
/cursos                     # Listagem geral
/cursos/programacao         # Por categoria
/cursos/programacao/python  # Subcategoria
/curso/python-para-iniciantes  # Página do curso
/blog                       # Blog
/blog/como-aprender-python  # Post
/categorias                 # Lista de categorias
/sobre                      # Sobre
/contato                    # Contato
/divulgue-seu-curso         # Submissão
```

### 6.2 Meta Tags Template

```tsx
// Curso
title: "{Nome do Curso} | habilite.me"
description: "{Descrição curta, max 155 chars}"

// Categoria
title: "Cursos de {Categoria} Online Gratuitos e Pagos | habilite.me"
description: "Encontre os melhores cursos de {categoria}. Compare preços e avaliações..."

// Blog Post
title: "{Título do Post} | Blog habilite.me"
description: "{Resumo do post, max 155 chars}"
```

### 6.3 JSON-LD Schemas

**Course:**
```json
{
  "@context": "https://schema.org",
  "@type": "Course",
  "name": "Nome do Curso",
  "description": "Descrição",
  "provider": {
    "@type": "Organization",
    "name": "Udemy"
  },
  "aggregateRating": {
    "@type": "AggregateRating",
    "ratingValue": "4.5",
    "reviewCount": "150"
  },
  "offers": {
    "@type": "Offer",
    "price": "0",
    "priceCurrency": "BRL"
  }
}
```

**ItemList (Listagem):**
```json
{
  "@context": "https://schema.org",
  "@type": "ItemList",
  "itemListElement": [
    {
      "@type": "ListItem",
      "position": 1,
      "item": {
        "@type": "Course",
        "name": "...",
        "url": "..."
      }
    }
  ]
}
```

### 6.4 Sitemap

Sitemap dinâmico gerado por Next.js:
- Páginas estáticas
- Todos os cursos aprovados
- Todas as categorias ativas
- Todos os posts publicados

---

## 7. Deploy & Infraestrutura

### 7.1 Docker Compose

```yaml
version: '3.8'

services:
  postgres:
    image: postgres:16-alpine
    container_name: habilite-db
    restart: unless-stopped
    environment:
      POSTGRES_USER: ${DB_USER}
      POSTGRES_PASSWORD: ${DB_PASSWORD}
      POSTGRES_DB: ${DB_NAME}
    volumes:
      - postgres_data:/var/lib/postgresql/data
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U ${DB_USER}"]
      interval: 10s
      timeout: 5s
      retries: 5

  strapi:
    build: ./apps/cms
    container_name: habilite-strapi
    restart: unless-stopped
    environment:
      DATABASE_CLIENT: postgres
      DATABASE_HOST: postgres
      DATABASE_PORT: 5432
      DATABASE_NAME: ${DB_NAME}
      DATABASE_USERNAME: ${DB_USER}
      DATABASE_PASSWORD: ${DB_PASSWORD}
      JWT_SECRET: ${JWT_SECRET}
      ADMIN_JWT_SECRET: ${ADMIN_JWT_SECRET}
      APP_KEYS: ${APP_KEYS}
    volumes:
      - strapi_uploads:/app/public/uploads
    depends_on:
      postgres:
        condition: service_healthy
    labels:
      - "traefik.enable=true"
      - "traefik.http.routers.strapi.rule=Host(`cms.habilite.me`)"

  web:
    build: ./apps/web
    container_name: habilite-web
    restart: unless-stopped
    environment:
      NEXT_PUBLIC_STRAPI_URL: https://cms.habilite.me
      STRAPI_API_TOKEN: ${STRAPI_API_TOKEN}
    depends_on:
      - strapi
    labels:
      - "traefik.enable=true"
      - "traefik.http.routers.web.rule=Host(`habilite.me`)"

volumes:
  postgres_data:
  strapi_uploads:
```

### 7.2 Environment Variables

```env
# Database
DB_USER=habilite
DB_PASSWORD=secure_password
DB_NAME=habilite

# Strapi
JWT_SECRET=random_string
ADMIN_JWT_SECRET=random_string
APP_KEYS=key1,key2

# Next.js
NEXT_PUBLIC_STRAPI_URL=https://cms.habilite.me
STRAPI_API_TOKEN=generated_token
NEXT_PUBLIC_SITE_URL=https://habilite.me
```

### 7.3 Coolify Configuration

```
# Web (Next.js)
Name: habilite-web
Port: 3000
Domain: habilite.me
SSL: Let's Encrypt

# Strapi
Name: habilite-strapi
Port: 1337
Domain: cms.habilite.me
SSL: Let's Encrypt
```

---

## 8. Roadmap de Execução

### FASE 1: Setup (3-4 dias)

#### Dia 1: Infraestrutura
- [ ] Criar repositório Git
- [ ] Configurar projeto Next.js com TypeScript
- [ ] Configurar Tailwind CSS
- [ ] Setup ESLint + Prettier
- [ ] Criar estrutura de pastas

#### Dia 2: Strapi
- [ ] Criar projeto Strapi
- [ ] Configurar PostgreSQL
- [ ] Criar collections (Cursos, Categorias, Reviews, Posts, Submissions)
- [ ] Configurar componente SEO
- [ ] Criar API tokens

#### Dia 3-4: Deploy Inicial
- [ ] Configurar Docker Compose
- [ ] Deploy no Coolify
- [ ] Configurar domínios (habilite.me, cms.habilite.me)
- [ ] Configurar SSL
- [ ] Configurar Cloudflare

---

### FASE 2: Frontend Base (5-7 dias)

#### Dia 5-6: Design System & UI
- [ ] Configurar variáveis CSS (cores, tipografia, spacing)
- [ ] Criar componentes UI base (Button, Card, Input, Badge)
- [ ] Criar StarRating, PriceTag, PlatformBadge
- [ ] Criar Skeleton components

#### Dia 7-8: Layout
- [ ] Criar Header (logo, nav, busca, mobile menu)
- [ ] Criar Footer (links, newsletter, social)
- [ ] Criar Breadcrumbs
- [ ] Layout responsivo

#### Dia 9-11: Páginas de Cursos
- [ ] Strapi client (lib/strapi/client.ts)
- [ ] Types (Course, Category, etc.)
- [ ] CourseCard component
- [ ] CourseGrid component
- [ ] Página /cursos (listagem)
- [ ] Página /cursos/[categoria]
- [ ] CourseFilters component
- [ ] CourseSearch component

---

### FASE 3: Página do Curso (3-4 dias)

#### Dia 12-13: Detalhes do Curso
- [ ] Página /curso/[slug]
- [ ] Hero section (imagem, título, preço, CTA)
- [ ] Seção de informações
- [ ] Descrição completa
- [ ] RelatedCourses component

#### Dia 14-15: Reviews
- [ ] ReviewList component
- [ ] ReviewForm component
- [ ] ReviewSummary component
- [ ] API route para submit review
- [ ] Integração com Strapi

---

### FASE 4: SEO & Meta (2-3 dias)

#### Dia 16-17: Meta Tags
- [ ] generateMetadata() em todas as páginas
- [ ] Open Graph tags
- [ ] Twitter cards
- [ ] Favicon e app icons

#### Dia 18: Schema.org
- [ ] JSON-LD para Course
- [ ] JSON-LD para ItemList
- [ ] JSON-LD para Organization
- [ ] JSON-LD para WebSite

#### Dia 19: Sitemap & Robots
- [ ] sitemap.ts dinâmico
- [ ] robots.ts
- [ ] Configurar Google Search Console

---

### FASE 5: Blog (3-4 dias)

#### Dia 20-21: Blog
- [ ] PostCard component
- [ ] Página /blog (listagem)
- [ ] Página /blog/[slug]
- [ ] PostContent component (rich text)
- [ ] JSON-LD para BlogPosting

#### Dia 22-23: Páginas Estáticas
- [ ] Página /sobre
- [ ] Página /contato (com formulário)
- [ ] Página /categorias
- [ ] Página /divulgue-seu-curso

---

### FASE 6: Home & Polish (2-3 dias)

#### Dia 24-25: Home Page
- [ ] Hero section com busca
- [ ] Cursos em destaque
- [ ] Categorias populares
- [ ] Como funciona
- [ ] Posts recentes
- [ ] CTA divulgue curso
- [ ] Newsletter form

#### Dia 26: Polish
- [ ] Loading states (loading.tsx)
- [ ] Error handling (error.tsx)
- [ ] 404 page (not-found.tsx)
- [ ] Animações e transições
- [ ] Testes manuais completos

---

### FASE 7: Conteúdo & Lançamento (3-4 dias)

#### Dia 27-28: Conteúdo Inicial
- [ ] Cadastrar 30-50 cursos manualmente
- [ ] Criar categorias principais
- [ ] Escrever 5 posts para o blog
- [ ] Criar página Sobre definitiva

#### Dia 29-30: Testes & Lançamento
- [ ] Testes de performance (Lighthouse)
- [ ] Testes de SEO
- [ ] Testes de responsividade
- [ ] Testes de acessibilidade (axe)
- [ ] Configurar Analytics
- [ ] **Lançamento! 🚀**

---

## 9. Métricas de Sucesso

### KPIs Técnicos

| Métrica | Target |
|---------|--------|
| LCP | < 2.5s |
| FID | < 100ms |
| CLS | < 0.1 |
| PageSpeed Mobile | 90+ |
| Lighthouse SEO | 100 |
| Lighthouse Accessibility | 90+ |

### KPIs de Negócio (Mês 1)

| Métrica | Target |
|---------|--------|
| Cursos cadastrados | 50+ |
| Posts no blog | 10+ |
| Visitas | 1.000+ |
| Keywords rankeando | 20+ |

---

## 10. Checklist de Lançamento

### Técnico
- [ ] HTTPS funcionando
- [ ] Domínios configurados
- [ ] SSL válido
- [ ] Performance OK (Lighthouse 90+)
- [ ] Mobile responsivo
- [ ] Sem erros no console

### SEO
- [ ] robots.txt acessível
- [ ] sitemap.xml gerado
- [ ] Google Search Console configurado
- [ ] Meta tags em todas as páginas
- [ ] JSON-LD validado
- [ ] Canonical URLs corretas

### Conteúdo
- [ ] Mínimo 30 cursos
- [ ] Mínimo 5 posts
- [ ] Página Sobre preenchida
- [ ] Imagens otimizadas

### Legal
- [ ] Termos de Uso
- [ ] Política de Privacidade
- [ ] Aviso de cookies (se necessário)

---

**Versão:** 1.0  
**Data:** Janeiro 2025  
**Status:** Planejamento
