# Módulo de Nivelamento SAEP — Gestão de Clientes e Grupos de Atendimento

**Clínica Pediátrica Infantil "Pequenos Passos"**  
Curso Técnico em Desenvolvimento de Sistemas | Unidade Curricular: Desenvolvimento de Sistemas Web SSR

---

## Tecnologias

| Tecnologia | Uso |
|------------|-----|
| Node.js + ES6 Modules | Runtime e padrão de módulos |
| Express | Framework web / rotas |
| EJS | Engine de templates (SSR) |
| PostgreSQL | Banco de dados relacional |
| bcrypt | Hash de senhas (10 rounds) |
| express-session | Controle de sessão |

---

## Requisitos Atendidos

### Funcionais
- **RF01** — Login com CPF e Senha + sessão
- **RF02** — CRUD completo de Grupos de Atendimento
- **RF03** — CRUD completo de Clientes (com FK)
- **RF04** — `<select>` dinâmico de grupos no formulário de cliente
- **RF05** — Busca filtrada por nome (`?busca=termo` + `ILIKE`)

### Não-Funcionais
- **RNF01** — SSR puro (sem `fetch()`, sem manipulação de DOM no cliente)
- **RNF02** — ES6 Modules (`"type": "module"`)
- **RNF03** — bcrypt (10 rounds)
- **RNF04** — Middleware de proteção de rotas com `express-session`

---

## Como executar

### 1. Criar o banco de dados

```bash
# No psql ou pgAdmin
createdb nivelamento_saep

# Executar o script de schema
psql -U postgres -d nivelamento_saep -f schema_nivelamento.sql
```

### 2. Configurar variáveis de ambiente

```bash
cp .env.example .env
# Edite .env se necessário (usuário, senha do PostgreSQL etc.)
```

### 3. Instalar dependências e iniciar

```bash
npm install
npm start
```

Acesse: **http://localhost:3000**

### Credenciais de acesso

| Campo | Valor |
|-------|-------|
| CPF   | `000.000.000-00` |
| Senha | `admin123` |

---

## Estrutura de pastas

```
projeto-nivelamento/
├── package.json
├── schema_nivelamento.sql
├── .env.example
├── DOCUMENTACAO.md
├── README.md
├── src/
│   ├── app.js
│   ├── config/db.js
│   ├── middleware/auth.js
│   └── routes/
│       ├── auth.js
│       ├── grupos.js
│       └── clientes.js
├── views/
│   ├── partials/
│   ├── auth/
│   ├── grupos/
│   ├── clientes/
│   └── dashboard.ejs
└── public/style.css
```

---

## Diagrama Entidade-Relacionamento (resumo)

- **grupos** (1) ──< (N) **clientes** (FK `grupo_id` com `ON DELETE RESTRICT`)
- **usuarios** (independente — autenticação)

---

## Critérios de Avaliação (Anexo 2) — Cobertura

| Critério | Pontos | Status |
|----------|--------|--------|
| Documentação e Modelagem (Anexo 1 + DER 1:N) | 10 | ✅ |
| Banco de Dados (DDL/DML + PK/FK + hash) | 15 | ✅ |
| Autenticação e Criptografia (bcrypt.compare + sessão) | 15 | ✅ |
| Proteção de Rotas (middleware → /login) | 15 | ✅ |
| CRUD de Grupos | 15 | ✅ |
| CRUD Relacional de Clientes (select + LEFT JOIN) | 20 | ✅ |
| Filtro de Pesquisa (ILIKE) e Usabilidade | 10 | ✅ |
| **Total** | **100** | **Completo** |
