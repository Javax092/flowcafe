# SAD — Software Architecture Document

# Flow Café

**Versão:** 1.0
**Status:** Planejamento técnico
**Produto:** Flow Café
**Empresa:** FLOWTECHAM

---

# 1. Objetivo

Este documento define a arquitetura técnica do Flow Café, garantindo que o MVP seja desenvolvido com qualidade, segurança, organização e capacidade de evolução.

O objetivo é evitar improvisação, acoplamento excessivo, código difícil de manter e decisões que prejudiquem a escalabilidade futura do produto.

---

# 2. Visão Arquitetural

O Flow Café será um sistema web responsivo no formato **PWA**, desenvolvido com arquitetura modular por domínio.

A aplicação será construída com foco em:

* segurança;
* manutenibilidade;
* clareza;
* escalabilidade;
* rastreabilidade;
* experiência rápida para operação diária.

---

# 3. Stack Técnica

## Frontend

* Next.js App Router
* React
* TypeScript
* Tailwind CSS
* PWA
* Server Components
* Client Components apenas quando necessário

## Backend

* Next.js Route Handlers
* Server Actions quando fizer sentido
* Prisma ORM
* PostgreSQL
* Zod para validação

## Autenticação

* JWT
* Cookie HttpOnly
* Middleware
* RBAC

## Infraestrutura

* Vercel
* Neon PostgreSQL ou Supabase PostgreSQL
* GitHub
* GitHub Actions futuramente

---

# 4. Princípios Arquiteturais

* Regra de negócio fica no servidor.
* Cliente nunca calcula valor financeiro final.
* APIs sempre validam entrada com Zod.
* Toda operação crítica gera auditoria.
* Código organizado por domínio.
* Componentes reutilizáveis ficam em shared.
* Dados sensíveis nunca aparecem em logs.
* Excluir dados financeiros fisicamente é proibido.
* O sistema deve nascer preparado para multiempresa.
* O MVP deve ser simples, mas não amador.

---

# 5. Organização de Pastas

```text
src/
  app/
    (auth)/
    (dashboard)/
    api/

  domains/
    auth/
      components/
      services/
      repositories/
      schemas/
      types/
      actions/
      permissions.ts

    dashboard/
      components/
      services/
      repositories/
      schemas/
      types/

    products/
      components/
      services/
      repositories/
      schemas/
      types/

    sales/
      components/
      services/
      repositories/
      schemas/
      types/

    cash/
      components/
      services/
      repositories/
      schemas/
      types/

    reports/
      components/
      services/
      repositories/
      schemas/
      types/

    users/
      components/
      services/
      repositories/
      schemas/
      types/

    audit/
      services/
      repositories/
      types/

  shared/
    components/
    hooks/
    lib/
    utils/
    constants/
    config/
    types/

  server/
    db/
    auth/
    middleware/
    errors/
    logger/

prisma/
  schema.prisma
  migrations/
  seed.ts

docs/
  PRD.md
  SAD.md
  SECURITY.md
  ROADMAP.md
```

---

# 6. Camadas do Sistema

## App Layer

Responsável por:

* rotas;
* páginas;
* layouts;
* handlers;
* composição visual.

Não deve conter regra de negócio pesada.

---

## Domain Layer

Responsável por:

* regras de negócio;
* serviços;
* schemas;
* tipos;
* repositórios;
* permissões.

---

## Infrastructure Layer

Responsável por:

* Prisma;
* conexão com banco;
* autenticação;
* logger;
* tratamento de erro;
* integrações externas futuras.

---

## Shared Layer

Responsável por:

* componentes genéricos;
* helpers;
* constantes;
* hooks reutilizáveis;
* tipos globais.

---

# 7. Domínios

## Auth

Responsável por:

* login;
* logout;
* sessão;
* JWT;
* permissões;
* proteção de rotas.

---

## Products

Responsável por:

* produtos;
* categorias;
* preços;
* status ativo/inativo.

---

## Sales

Responsável por:

* criação de venda;
* itens da venda;
* pagamento;
* cancelamento;
* histórico.

---

## Cash

Responsável por:

* abertura de caixa;
* sangria;
* reforço;
* fechamento;
* conferência.

---

## Dashboard

Responsável por:

* indicadores;
* resumo diário;
* últimas vendas;
* dados em tempo real.

---

## Reports

Responsável por:

* relatórios diários;
* relatórios por período;
* exportações futuras.

---

## Audit

Responsável por:

* logs de ações críticas;
* rastreabilidade;
* histórico de alterações.

---

# 8. Autenticação

A autenticação utilizará JWT armazenado em cookie HttpOnly.

## Regras

* Não usar localStorage.
* Não validar sessão no client.
* Middleware protege rotas privadas.
* Sessão deve carregar userId, businessId e role.
* Role nunca vem do client.
* Senhas devem ser armazenadas com hash seguro.

## Papéis

```text
ADMIN
MANAGER
ATTENDANT
```

---

# 9. Autorização

A autorização será baseada em RBAC.

## ADMIN

Pode executar todas as ações.

## MANAGER

Pode:

* abrir caixa;
* fechar caixa;
* vender;
* cancelar venda;
* visualizar relatórios.

## ATTENDANT

Pode:

* vender;
* visualizar PDV;
* consultar produtos ativos.

Não pode:

* alterar preços;
* fechar caixa;
* acessar relatórios administrativos.

---

# 10. Banco de Dados

O banco será PostgreSQL com Prisma.

## Entidades principais

```text
Business
User
Category
Product
Sale
SaleItem
Payment
CashSession
CashMovement
AuditLog
```

## Regras

* Todas as tabelas operacionais possuem businessId.
* Valores financeiros usam Decimal.
* Operações financeiras usam transação.
* Vendas não são apagadas fisicamente.
* Cancelamentos são registrados.
* Índices devem ser criados para businessId, createdAt, status e dailyDate.

---

# 11. Estratégia Multiempresa

Mesmo no MVP, o sistema deve ser preparado para multiempresa.

Toda consulta operacional deve filtrar por:

```text
businessId
```

Nunca buscar dados globais sem filtro de empresa.

---

# 12. Datas e Timezone

Timezone oficial:

```text
America/Manaus
```

Regras:

* Relatórios usam data operacional.
* Caixa possui dailyDate.
* Venda possui createdAt e dailyDate.
* Dashboard usa dailyDate.
* Nunca depender apenas do timezone do servidor.

---

# 13. Padrão de APIs

## Exemplo

```text
GET /api/products
POST /api/products
PATCH /api/products/:id
DELETE /api/products/:id

POST /api/sales
GET /api/sales/today
POST /api/sales/:id/cancel

GET /api/cash/current
POST /api/cash/open
POST /api/cash/movement
POST /api/cash/close
```

## Regras

* Toda entrada validada com Zod.
* Toda resposta de erro padronizada.
* Toda rota protegida deve usar sessão do servidor.
* Toda operação crítica deve gerar AuditLog.

---

# 14. Tratamento de Erros

Erros devem seguir padrão:

```json
{
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Dados inválidos.",
    "details": []
  }
}
```

## Códigos sugeridos

```text
UNAUTHORIZED
FORBIDDEN
VALIDATION_ERROR
NOT_FOUND
BUSINESS_RULE_ERROR
INTERNAL_ERROR
```

---

# 15. Segurança

## Obrigatório

* Cookie HttpOnly.
* SameSite Lax.
* Secure em produção.
* Validação com Zod.
* RBAC.
* Proteção de rotas.
* Hash de senha.
* Sem segredos no GitHub.
* .env.example sem valores reais.
* Logs sem dados sensíveis.
* Middleware em rotas privadas.
* Regras financeiras no servidor.

---

# 16. Auditoria

A tabela AuditLog deve registrar:

* usuário;
* empresa;
* ação;
* entidade;
* entidadeId;
* dados relevantes;
* IP quando disponível;
* user agent quando disponível;
* data/hora.

## Eventos auditáveis

* login;
* abertura de caixa;
* sangria;
* reforço;
* fechamento de caixa;
* venda criada;
* venda cancelada;
* produto criado;
* produto alterado;
* usuário criado;
* alteração de permissão.

---

# 17. Transações

Usar transação Prisma em:

* criação de venda;
* cancelamento de venda;
* fechamento de caixa;
* movimentação de caixa;
* ajustes financeiros.

Regra:

Nenhuma venda pode ser parcialmente salva.

---

# 18. Padrão de Código

## Nomenclatura

* Componentes: PascalCase
* Funções: camelCase
* Constantes: UPPER_CASE
* Tipos: PascalCase
* Arquivos: kebab-case ou camelCase, mantendo consistência

## TypeScript

* Evitar `any`.
* Preferir tipos explícitos em regras de negócio.
* Usar inferência apenas quando clara.
* Validar entrada com Zod.

---

# 19. UI/UX

O sistema deve priorizar velocidade operacional.

## PDV

* poucos cliques;
* botões grandes;
* visual claro;
* carrinho sempre visível;
* feedback rápido;
* bloqueio visual quando caixa fechado.

## Dashboard

* indicadores grandes;
* leitura rápida;
* atualização automática;
* alertas visíveis.

## Mobile

* navegação simples;
* toque confortável;
* carrinho fixo;
* sem telas poluídas.

---

# 20. Performance

## Metas

* Login abaixo de 1 segundo.
* Dashboard carregando abaixo de 2 segundos.
* Venda registrada abaixo de 500 ms em ambiente ideal.
* APIs simples abaixo de 300 ms.

## Estratégias

* Consultas filtradas por businessId.
* Índices adequados.
* Evitar overfetching.
* Server Components para dados estáticos.
* Client Components apenas para interação.

---

# 21. Tempo Real

No MVP, o tempo real será feito por polling controlado.

## Estratégia

Dashboard atualiza a cada:

```text
10 a 15 segundos
```

No futuro poderá evoluir para:

* WebSocket;
* Server-Sent Events;
* Redis Pub/Sub.

---

# 22. Testes

## Prioridade no MVP

* regras de negócio;
* criação de venda;
* fechamento de caixa;
* permissões;
* validações;
* cálculo de totais.

## Tipos

* testes unitários;
* testes de integração;
* testes manuais documentados.

---

# 23. CI/CD

## MVP

Validações locais obrigatórias:

```bash
npm run lint
npm run typecheck
npm run build
npx prisma validate
```

## Futuro

GitHub Actions:

```text
Pull Request
↓
Lint
↓
Typecheck
↓
Build
↓
Prisma validate
↓
Testes
```

---

# 24. Git e Branches

## Branches

```text
main
develop
feature/*
fix/*
release/*
hotfix/*
```

## Commits

Seguir Conventional Commits:

```text
feat:
fix:
chore:
docs:
refactor:
test:
style:
```

Exemplos:

```bash
git commit -m "feat: add cash session workflow"
git commit -m "feat: implement POS sales flow"
git commit -m "docs: add software architecture document"
```

---

# 25. Documentação

Arquivos obrigatórios:

```text
README.md
.env.example
docs/PRD.md
docs/SAD.md
docs/SECURITY.md
docs/ROADMAP.md
```

O README deve conter:

* visão do projeto;
* stack;
* instalação;
* variáveis de ambiente;
* comandos;
* arquitetura;
* fluxo de desenvolvimento;
* deploy.

---

# 26. Deploy

## Ambientes

```text
local
staging
production
```

## Regras

* staging para homologação;
* production apenas com build validado;
* variáveis separadas por ambiente;
* banco de produção nunca usado localmente.

---

# 27. Observabilidade

No MVP:

* logs de erro;
* audit logs;
* mensagens padronizadas.

Futuro:

* Sentry;
* métricas;
* monitoramento de uptime;
* alertas.

---

# 28. Riscos Técnicos

## Risco

Regras financeiras no frontend.

Mitigação:

Todas as regras financeiras no servidor.

---

## Risco

Mistura de domínio com UI.

Mitigação:

Arquitetura modular por domínio.

---

## Risco

Dados entre empresas vazando.

Mitigação:

Filtro obrigatório por businessId.

---

## Risco

Caixa inconsistente.

Mitigação:

Transações e validações.

---

## Risco

Projeto crescer desorganizado.

Mitigação:

Docs, padrões e revisão por sprint.

---

# 29. Critérios de Aceite Técnico

O MVP só pode ser considerado pronto quando:

* login funciona;
* permissões funcionam;
* produto pode ser cadastrado;
* caixa pode ser aberto e fechado;
* venda pode ser registrada;
* venda não ocorre sem caixa aberto;
* dashboard mostra dados reais;
* relatório diário confere;
* build passa;
* TypeScript passa;
* Prisma valida;
* código não contém segredo;
* GitHub está organizado.

---

# 30. Direção Futura

Após o MVP:

* estoque;
* custos;
* lucro;
* metas;
* WhatsApp;
* IA;
* previsão de demanda;
* assinaturas;
* multiempresa completa;
* app nativo.
