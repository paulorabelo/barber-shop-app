# 💈 Barber Shop App — Monorepo Full-Stack

![License](https://img.shields.io/badge/license-MIT-green)
![Turborepo](https://img.shields.io/badge/Turborepo-Monorepo-EF4444?logo=turborepo)
![Next.js](https://img.shields.io/badge/Next.js-14-black?logo=next.js)
![React](https://img.shields.io/badge/React-18-61DAFB?logo=react)
![NestJS](https://img.shields.io/badge/NestJS-10-E0234E?logo=nestjs)
![TypeScript](https://img.shields.io/badge/TypeScript-5-3178C6?logo=typescript)
![Tailwind](https://img.shields.io/badge/Tailwind-3-38B2AC?logo=tailwindcss)
![pnpm](https://img.shields.io/badge/pnpm-8-F69220?logo=pnpm)

> **Sistema completo de gerenciamento para barbearia** — Agendamentos, profissionais, serviços e clientes. Monorepo com **Next.js (Frontend)** + **NestJS (Backend)** gerenciado pelo **Turborepo**.

## 🏗️ Arquitetura do Monorepo

```
barber-shop-app/
├── apps/
│   ├── frontend/          # 🎨 Next.js 14 (App Router) + React 18
│   │   ├── src/
│   │   │   ├── components/    # UI components (Radix, Tailwind, Framer Motion)
│   │   │   ├── data/          # Hooks, Contextos (React Query/Context API)
│   │   │   └── app/           # Rotas Next.js App Router
│   │   └── tailwind.config.ts
│   │
│   └── backend/           # 🔧 NestJS 10 + TypeScript
│       ├── src/
│       │   ├── app.module.ts
│       │   ├── app.controller.ts
│       │   ├── app.service.ts
│       │   └── ... (módulos: agendamentos, profissionais, serviços, auth)
│       ├── test/            # E2E + Unit tests (Jest)
│       └── nest-cli.json
│
├── packages/
│   ├── ui/                # 📦 Componentes React compartilhados
│   ├── eslint-config/     # 🔧 Config ESLint (Next + Prettier)
│   └── typescript-config/ # 📝 tsconfig bases
│
├── turbo.json             # ⚙️ Pipeline Turborepo
├── package.json           # 📦 Workspace root (pnpm)
├── pnpm-lock.yaml
└── pnpm-workspace.yaml
```

## 🛠️ Stack Tecnológica

| Camada | Tecnologia | Versão | Finalidade |
|--------|------------|--------|------------|
| **Frontend** | Next.js | 14.2.5 | App Router, SSR, RSC |
| | React | 18 | UI Components |
| | Tailwind CSS | 3.4.1 | Styling utility-first |
| | Radix UI | 2.1.1 | Primitivos acessíveis |
| | Framer Motion | 11.3.17 | Animações |
| | Tabler Icons / Lucide | 3.11 / 0.416 | Ícones |
| **Backend** | NestJS | 10 | Framework Node.js modular |
| | TypeScript | 5.1.3 | Tipagem estática |
| | Jest | 29.5 | Testes unitários + E2E |
| | RxJS | 7.8.1 | Reactive streams |
| **Monorepo** | Turborepo | Latest | Build system + Remote caching |
| | pnpm | 8 | Package manager rápido |
| | ESLint + Prettier | Latest | Linting + Formatação |

## 🚀 Como Executar

### Pré-requisitos
- **Node.js** 18+ (recomendado 20 LTS)
- **pnpm** 8+ (
added 1 package in 7s

1 package is looking for funding
  run `npm fund` for details ou )
- **PostgreSQL** (para backend) ou Docker

### Instalação
```bash
# 1. Clone
git clone https://github.com/paulorabelo/barber-shop-app.git
cd barber-shop-app

# 2. Instale dependências (pnpm workspace)
pnpm install

# 3. Configure variáveis de ambiente
cp apps/backend/.env.example apps/backend/.env  # Configure DB, JWT, etc.
cp apps/frontend/.env.example apps/frontend/.env  # Configure API URL

# 4. Rode migrações (se usar Prisma/TypeORM no backend)
cd apps/backend && pnpm run migration:run

# 5. Desenvolvimento (todos os apps + packages)
pnpm dev
```

### URLs de Desenvolvimento
| App | URL |
|-----|-----|
| **Frontend** | http://localhost:3000 |
| **Backend API** | http://localhost:3001 (ou porta configurada) |
| **Swagger Docs** | http://localhost:3001/api/docs |

## 📦 Scripts Principais

```bash
# Desenvolvimento (roda frontend + backend em paralelo)
pnpm dev

# Build de produção (todos os apps + packages)
pnpm build

# Lint em todo o monorepo
pnpm lint

# Formatação com Prettier
pnpm format

# Testes (backend)
cd apps/backend && pnpm test
pnpm test:e2e
pnpm test:cov

# Limpar cache Turborepo
pnpm turbo run clean
# ou
pnpm exec turbo run clean
```

## 🔧 Configuração do Backend (apps/backend/.env)

```env
# Database
DATABASE_URL=postgresql://user:pass@localhost:5432/barber_shop?schema=public

# JWT
JWT_SECRET=seu-segredo-super-seguro
JWT_EXPIRES_IN=7d

# App
PORT=3001
NODE_ENV=development
FRONTEND_URL=http://localhost:3000

# Email (opcional - para notificações)
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_USER=seu@email.com
SMTP_PASS=sua-senha-app
```

## 🔧 Configuração do Frontend (apps/frontend/.env)

```env
NEXT_PUBLIC_API_URL=http://localhost:3001
NEXT_PUBLIC_APP_NAME=Barber Shop
```

## 🐳 Docker (Opcional)

```bash
# Subir apenas banco de dados
docker-compose up -d postgres

# Ou stack completa (se docker-compose.yml existir na raiz)
docker-compose up -d
```

## 🧪 Testes

```bash
# Backend - Unitários
cd apps/backend && pnpm test

# Backend - E2E
cd apps/backend && pnpm test:e2e

# Backend - Coverage
cd apps/backend && pnpm test:cov

# Frontend - Lint + Type Check
cd apps/frontend && pnpm lint && pnpm tsc --noEmit
```

## 📁 Estrutura de Módulos do Backend (Sugerida)

```
src/
├── auth/              # Autenticação (JWT, Guards, Decorators)
├── users/             # Usuários (Clientes, Admins)
├── professionals/     # Profissionais (Barbeiros)
├── services/          # Serviços (Corte, Barba, etc.)
├── appointments/      # Agendamentos (CRUD, Conflitos, Notificações)
├── schedule/          # Horários/Disponibilidade
├── payments/          # Pagamentos (integração futura)
└── common/            # DTOs, Pipes, Guards, Interceptors compartilhados
```

## 🌐 Deploy

### Frontend (Vercel - Recomendado)
```bash
# Conecte o repo no Vercel
# Root Directory: apps/frontend
# Build Command: pnpm build
# Output Directory: .next
```

### Backend (Railway / Render / Fly.io / AWS)
```bash
# Build
pnpm --filter backend build

# Start
node apps/backend/dist/main.js
```

### Turborepo Remote Caching (Vercel)
```bash
npx turbo login
npx turbo link
```

## 🤝 Contribuindo

1. **Fork** o projeto
2. **Branch**: 
3. **Commits Convencionais**:
   -  nova funcionalidade
   -  correção de bug
   -  documentação
   -  refatoração
   -  testes
   -  manutenção
4. **Push**: 
5. **Pull Request**

### Padrões de Código
- **TypeScript strict mode** em todo monorepo
- **ESLint + Prettier** configurados no 
- **Husky** (opcional) para pre-commit hooks
- **Conventional Commits** obrigatórios

## 📄 Licença

**MIT License** — Veja [LICENSE](LICENSE).

## 👨‍💻 Autor

**Paulo Rabelo**
- GitHub: [@paulorabelo](https://github.com/paulorabelo)
- Blog: [blog.paulorabelo.dev.com.br](https://blog.paulorabelo.dev.com.br)
- LinkedIn: [Paulo Rabelo](https://www.linkedin.com/in/paulorabelooficial/)

---

<div align="center">
  <sub>Monorepo Full-Stack para barbearia moderna 💈</sub><br>
  <sub><a href="https://github.com/paulorabelo/barber-shop-app">⭐ Star se este projeto te inspira!</a></sub>
</div>
