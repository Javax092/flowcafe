# Product Requirements Document

# PRD — Flow Café

**Versão:** 1.0
**Status:** Planejamento
**Produto:** Flow Café
**Empresa:** FLOWTECHAM

---

# 1. Visão do Produto

O Flow Café é uma plataforma SaaS desenvolvida para digitalizar e controlar a operação diária de cafeterias, cafés da manhã, padarias, lanchonetes e pequenos restaurantes.

O objetivo é transformar processos manuais em um fluxo operacional simples, confiável e orientado por dados, permitindo que o proprietário acompanhe toda a operação em tempo real.

O sistema será desenvolvido inicialmente como um **PWA (Progressive Web App)** responsivo, preparado para evoluir para aplicações móveis nativas futuramente.

---

# 2. Problema

Grande parte dos pequenos estabelecimentos ainda controla suas vendas utilizando papel, calculadoras, planilhas ou aplicativos genéricos.

Esses processos geram:

- dificuldade para acompanhar o faturamento;
- erros de caixa;
- falta de controle financeiro;
- perda de produtos;
- pouca visibilidade sobre vendas;
- dificuldade para tomar decisões;
- ausência de indicadores de desempenho.

---

# 3. Objetivos do Produto

O sistema deve permitir que o proprietário consiga:

- acompanhar a operação em tempo real;
- controlar caixa;
- registrar vendas rapidamente;
- acompanhar formas de pagamento;
- visualizar indicadores;
- reduzir erros operacionais;
- gerar relatórios automáticos;
- preparar a empresa para crescimento.

---

# 4. Objetivos de Negócio

- Reduzir erros operacionais.
- Diminuir tempo de fechamento do caixa.
- Aumentar o controle financeiro.
- Criar um produto SaaS escalável.
- Permitir cobrança recorrente por assinatura.
- Tornar-se referência para pequenos estabelecimentos alimentícios.

---

# 5. Público-Alvo

## Primário

- Cafeterias
- Casas de café regional
- Cafés da manhã
- Pequenas lanchonetes
- Padarias

## Secundário

- Quiosques
- Food trucks
- Restaurantes compactos

---

# 6. Personas

## Dono

Objetivo:

Ter controle financeiro da empresa.

Necessidades:

- acompanhar vendas;
- acompanhar caixa;
- saber quanto faturou;
- acompanhar funcionários;
- visualizar relatórios.

---

## Gerente

Objetivo:

Controlar a operação diária.

Necessidades:

- abrir caixa;
- fechar caixa;
- acompanhar equipe;
- corrigir erros.

---

## Atendente

Objetivo:

Registrar pedidos rapidamente.

Necessidades:

- interface simples;
- poucos cliques;
- rapidez;
- estabilidade.

---

# 7. Proposta de Valor

"O proprietário sabe exatamente como está sua operação em qualquer momento do dia."

---

# 8. Escopo MVP

## Incluído

### Login

- autenticação
- sessão segura
- controle de acesso

---

### Dashboard

- faturamento do dia
- quantidade de pedidos
- ticket médio
- caixa aberto
- últimas vendas
- vendas por pagamento

---

### Produtos

- cadastro
- edição
- exclusão lógica
- categorias

---

### PDV

- venda rápida
- múltiplos itens
- observações
- descontos
- pagamento
- confirmação

---

### Caixa

- abertura
- sangria
- reforço
- fechamento
- histórico

---

### Relatórios

- vendas do dia
- vendas por período
- formas de pagamento
- produtos vendidos

---

# 9. Fora do MVP

- emissão fiscal;
- integração bancária;
- PIX automático;
- estoque inteligente;
- IA;
- aplicativo nativo;
- integração com delivery;
- integração com contabilidade;
- programa de fidelidade;
- WhatsApp automático.

---

# 10. Perfis

## ADMIN

Pode acessar tudo.

---

## MANAGER

Pode operar caixa.

Pode visualizar relatórios.

Pode corrigir vendas.

---

## ATTENDANT

Pode registrar vendas.

Não pode alterar preços.

Não pode fechar caixa.

---

# 11. Fluxo Principal

Login

↓

Abrir Caixa

↓

Registrar Venda

↓

Receber Pagamento

↓

Atualizar Dashboard

↓

Registrar Auditoria

↓

Fechar Caixa

↓

Gerar Relatório

---

# 12. Funcionalidades

## Login

Critério de aceite

- autenticação segura;
- sessão persistente;
- logout.

---

## Produtos

Critério de aceite

- CRUD completo;
- validações;
- categorias.

---

## PDV

Critério de aceite

- adicionar produto;
- alterar quantidade;
- remover item;
- desconto;
- observação;
- finalizar venda.

---

## Caixa

Critério de aceite

- apenas um caixa aberto;
- fechamento obrigatório;
- diferença registrada.

---

## Dashboard

Critério de aceite

Atualização automática.

Indicadores corretos.

Sem dados duplicados.

---

# 13. Regras de Negócio

- Venda somente com caixa aberto.
- Produto inativo não pode ser vendido.
- Toda venda pertence a um usuário.
- Toda venda pertence a uma empresa.
- Todo cancelamento exige motivo.
- Todo cancelamento gera auditoria.
- Valores financeiros nunca são calculados no cliente.
- Timezone operacional: America/Manaus.
- Valores monetários utilizam Decimal.
- Exclusão física de vendas não é permitida.

---

# 14. Requisitos Não Funcionais

## Performance

- Dashboard < 2 segundos.
- Venda registrada < 500 ms.
- APIs < 300 ms (meta para operações simples).

---

## Segurança

- JWT HttpOnly.
- Middleware.
- RBAC.
- Zod.
- Proteção CSRF.
- Auditoria.
- Criptografia de senha com Argon2 ou bcrypt.

---

## Disponibilidade

Objetivo:

99,5%.

---

## Escalabilidade

Preparado para:

- múltiplas empresas;
- milhares de vendas;
- múltiplos usuários simultâneos.

---

## Responsividade

Desktop.

Tablet.

Celular.

---

# 15. Arquitetura Técnica

Frontend

Next.js App Router

TypeScript

Tailwind CSS

Server Components

PWA

Backend

Route Handlers

Server Actions quando apropriado

Prisma ORM

PostgreSQL

Autenticação

JWT

Cookies HttpOnly

RBAC

Banco

PostgreSQL

Prisma

Migrations

Deploy

Frontend

Vercel

Banco

Neon PostgreSQL

---

# 16. Estrutura Inicial de Domínios

- Auth
- Dashboard
- Products
- Sales
- Cash
- Reports
- Users
- Settings
- Audit

Cada domínio deve conter:

- components
- services
- repositories
- schemas
- hooks
- types
- api
- tests

---

# 17. Critérios de Qualidade

Todo código deverá:

- passar no ESLint;
- passar no TypeScript;
- passar no Build;
- possuir tipagem forte;
- evitar duplicação;
- seguir arquitetura modular;
- utilizar componentes reutilizáveis;
- possuir nomenclatura consistente;
- evitar funções excessivamente longas.

---

# 18. Roadmap

## Versão 1

- Login
- Dashboard
- Produtos
- Caixa
- PDV
- Relatórios

---

## Versão 2

- Estoque
- Funcionários
- Metas
- Custos
- Lucro

---

## Versão 3

- Multiempresa completa
- Assinaturas
- WhatsApp
- IA
- Previsões
- Integrações

---

# 19. Métricas de Sucesso

Operacionais:

- Tempo médio de registro de venda inferior a 15 segundos.
- Fechamento de caixa inferior a 5 minutos.
- Redução de erros de caixa.

Produto:

- Ativação em menos de 30 minutos.
- Retenção mensal superior a 90%.
- Disponibilidade superior a 99,5%.

Negócio:

- Crescimento consistente da base de clientes.
- Expansão para novos segmentos.
- Receita recorrente previsível.

---

# 20. Visão de Longo Prazo

O Flow Café deve evoluir para uma plataforma completa de gestão operacional para pequenos negócios de alimentação, mantendo como princípio central uma experiência extremamente simples para o operador e uma visão estratégica em tempo real para o proprietário, permitindo decisões rápidas, redução de desperdícios e crescimento sustentável.
