# Arquitetura do Sistema

## 🏗️ Visão Geral da Arquitetura

O sistema segue a arquitetura **MVC em Camadas (Layered Architecture)** para garantir separação de responsabilidades, manutenibilidade e escalabilidade.

```
┌─────────────────────────────────────────────────────────┐
│              CAMADA APRESENTAÇÃO (Frontend)              │
│  React + Vite + TailwindCSS + Axios                     │
├─────────────────────────────────────────────────────────┤
│  ┌─────────────────────────────────────────────────────┐
│  │          CAMADA API (Routes & Controllers)           │
│  │  Express.js + JWT Authentication                    │
│  └─────────────────────────────────────────────────────┘
│  ┌─────────────────────────────────────────────────────┐
│  │       CAMADA LÓGICA (Services & Business Logic)      │
│  │  Validações, Regras de Negócio, Geração de Relatórios
│  └─────────────────────────────────────────────────────┘
│  ┌─────────────────────────────────────────────────────┐
│  │    CAMADA DADOS (Models, Repositories & Database)    │
│  │  ORM (Sequelize), Queries, Transações                │
│  └─────────────────────────────────────────────────────┘
├─────────────────────────────────────────────────────────┤
│         CAMADA INFRAESTRUTURA & CONFIGURAÇÃO             │
│  Base de Dados, Cache, Logs, File Storage               │
└─────────────────────────────────────────────────────────┘
```

---

## 📁 Estrutura de Diretórios

```
Sistema-de-Gest-o-para-a-AMDAV-/
│
├── backend/                          # Servidor Node.js
│   ├── src/
│   │   ├── config/                  # Configurações
│   │   │   ├── database.js          # Conexão BD
│   │   │   ├── jwt.js               # Configuração JWT
│   │   │   └── multer.js            # Upload de ficheiros
│   │   │
│   │   ├── models/                  # Modelos de Dados
│   │   │   ├── User.js
│   │   │   ├── Direcao.js
│   │   │   ├── Atleta.js
│   │   │   ├── Modalidade.js
│   │   │   └── Parceiro.js
│   │   │
│   │   ├── routes/                  # Rotas API
│   │   │   ├── auth.routes.js       # Autenticação
│   │   │   ├── direcao.routes.js    # Módulo Direção
│   │   │   ├── atleta.routes.js     # Módulo Atletas
│   │   │   ├── parceiro.routes.js   # Módulo Parceiros
│   │   │   └── modalidade.routes.js # Modalidades
│   │   │
│   │   ├── controllers/             # Controllers
│   │   │   ├── authController.js
│   │   │   ├── direcaoController.js
│   │   │   ├── atletaController.js
│   │   │   ├── parceiroController.js
│   │   │   └── modalidadeController.js
│   │   │
│   │   ├── services/                # Lógica de Negócio
│   │   │   ├── authService.js
│   │   │   ├── atletaService.js     # Inclui relatórios
│   │   │   ├── parceiroService.js
│   │   │   ├── direcaoService.js
│   │   │   └── reportService.js     # Geração de PDF/Excel
│   │   │
│   │   ├── middleware/              # Middlewares
│   │   │   ├── auth.js              # JWT Validation
│   │   │   ├── errorHandler.js
│   │   │   └── validation.js
│   │   │
│   │   ├── utils/                   # Utilitários
│   │   │   ├── validators.js        # Validação de dados
│   │   │   ├── logger.js            # Logs
│   │   │   ├── fileUpload.js        # Gestão de uploads
│   │   │   └── constants.js         # Constantes
│   │   │
│   │   ├── exceptions/              # Exceções personalizadas
│   │   │   └── AppError.js
│   │   │
│   │   └── app.js                   # Configuração Express
│   │
│   ├── uploads/                     # Ficheiros carregados
│   │   ├── fotos/
│   │   └── documentos/
│   │
│   ├── .env.example                 # Variáveis de ambiente (exemplo)
│   ├── .env                         # Variáveis de ambiente (privado)
│   ├── server.js                    # Entrada do servidor
│   ├── package.json
│   └── package-lock.json
│
├── frontend/                         # Aplicação React
│   ├── src/
│   │   ├── components/              # Componentes Reutilizáveis
│   │   │   ├── Header.jsx
│   │   │   ├── Sidebar.jsx
│   │   │   ├── FormAthlete.jsx
│   │   │   ├── FormDirection.jsx
│   │   │   ├── FormPartner.jsx
│   │   │   └── Modal.jsx
│   │   │
│   │   ├── pages/                   # Páginas Principais
│   │   │   ├── Login.jsx
│   │   │   ├── Dashboard.jsx
│   │   │   ├── AtletasPage.jsx
│   │   │   ├── DirecaoPage.jsx
│   │   │   ├── ParceirosPage.jsx
│   │   │   └── NotFound.jsx
│   │   │
│   │   ├── services/                # Chamadas API
│   │   │   ├── api.js               # Instância Axios
│   │   │   ├── authService.js
│   │   │   ├── atletaService.js
│   │   │   ├── direcaoService.js
│   │   │   ├── parceiroService.js
│   │   │   └── reportService.js
│   │   │
│   │   ├── context/                 # Context API
│   │   │   ├── AuthContext.jsx
│   │   │   └── NotificationContext.jsx
│   │   │
│   │   ├── hooks/                   # Custom Hooks
│   │   │   ├── useAuth.js
│   │   │   ├── useFetch.js
│   │   │   └── useForm.js
│   │   │
│   │   ├── styles/                  # Estilos Globais
│   │   │   ├── globals.css
│   │   │   └── tailwind.config.js
│   │   │
│   │   ├── utils/                   # Utilitários
│   │   │   ├── formatters.js        # Formatação de dados
│   │   │   ├── validators.js        # Validação cliente
│   │   │   └── constants.js
│   │   │
│   │   └── App.jsx                  # Componente raiz
│   │
│   ├── public/
│   │   ├── index.html
│   │   └── favicon.ico
│   │
│   ├── .env.example
│   ├── .env
│   ├── vite.config.js
│   ├── package.json
│   └── package-lock.json
│
├── database/                        # Scripts BD
│   ├── schema.sql                   # Criação de tabelas
│   ├── seeds.sql                    # Dados iniciais
│   └── migrations/                  # Migrações
│
├── docs/                            # Documentação
│   ├── REQUISITOS.md
│   ├── BANCO_DADOS.md
│   ├── ARQUITETURA.md
│   ├── API.md                       # Documentação da API
│   └── SETUP.md                     # Guia de instalação
│
├── .gitignore
├── README.md
└── docker-compose.yml               # (Opcional) Containers
```

---

## 🔄 Fluxo de Dados

### Fluxo de Criação de Atleta

```
┌─────────────────────┐
│  Frontend (React)   │
│  Form Preenchido    │
└──────────┬──────────┘
           │ POST /api/atletas
           │ { nome, data_nasc, ... }
           ▼
┌──────────────────────────────┐
│   Backend API (Express)      │
│   POST /api/atletas          │
└──────────┬───────────────────┘
           │ atletaController.create()
           ▼
┌──────────────────────────────┐
│  Middleware de Validação     │
│  - JWT válido?               │
│  - Dados válidos?            │
│  - Upload OK?                │
└──────────┬───────────────────┘
           │ ✓ Validado
           ▼
┌──────────────────────────────┐
│  Service (Lógica)            │
│  atletaService.create()      │
│  - Validação extra           │
│  - Lógica de negócio         │
│  - Preparar dados            │
└──────────┬───────────────────┘
           │ Dados validados
           ▼
┌──────────────────────────────┐
│  Repository/Model            │
│  Atleta.create()             │
│  INSERT INTO atletas ...     │
└──────────┬───────────────────┘
           │
           ▼
┌──────────────────────────────┐
│  Base de Dados (PostgreSQL)  │
│  Guardar Atleta              │
└──────────┬───────────────────┘
           │ Sucesso
           ▼
┌──────────────────────────────┐
│  Response HTTP 201           │
│  { id, nome, modalidade }    │
└──────────┬───────────────────┘
           │
           ▼
┌──────────────────────────────┐
│  Frontend                    │
│  Mostrar mensagem sucesso    │
│  Atualizar lista             │
└──────────────────────────────┘
```

---

## 🔐 Autenticação JWT

### Fluxo de Autenticação

```
Usuario              API                      BD
   │                  │                       │
   │─ POST /login ──► │                       │
   │  {email, pass}   │                       │
   │                  │─ SELECT user ────────► │
   │                  │◄─ User encontrado ───│
   │                  │                       │
   │                  │ bcrypt.compare(pass)  │
   │                  │ ✓ Validado            │
   │                  │                       │
   │                  │ jwt.sign({            │
   │                  │   userId: 123,        │
   │                  │   perfil: 'gestor',   │
   │                  │   exp: +24h           │
   │                  │ })                    │
   │                  │                       │
   │◄─ 200 OK ────── │                       │
   │ {token,profile}  │                       │
   │                  │                       │

Requisições Subsequentes:
   │                  │                       │
   │─ GET /atletas ─► │ Authorization:        │
   │ com token        │ Bearer eyJhbGc...     │
   │                  │                       │
   │                  │ jwt.verify(token)     │
   │                  │ ✓ Token válido        │
   │                  │                       │
   │                  │─ SELECT atletas ────► │
   │                  │◄─ Dados ──────────── │
   │                  │                       │
   │◄─ 200 OK ────── │                       │
   │ [atletas...]     │                       │
   │                  │                       │
```

### Estrutura do JWT Token

```
Header: { alg: 'HS256', typ: 'JWT' }

Payload: {
  userId: 5,
  email: 'gestor@amdav.pt',
  perfil: 'gestor',          // admin, gestor, visualizador
  iat: 1621502000,
  exp: 1621588400            // Válido por 24h
}

Signature: HMACSHA256(
  base64UrlEncode(header) + "." +
  base64UrlEncode(payload),
  SECRET_KEY
)
```

---

## 🎯 Padrões de Projeto

### 1. MVC (Model-View-Controller)
- **Model:** Estrutura de dados (Atleta, Direção, Parceiro)
- **View:** Componentes React (Frontend)
- **Controller:** Lógica de request/response

### 2. Service Pattern
- Centraliza lógica de negócio
- Separação entre controller e dados
- Reutilização de código

### 3. Repository Pattern
- Abstração da base de dados
- Facilita testes e migrações
- Operações CRUD centralizadas

### 4. Middleware Pattern
- Validação de JWT
- Tratamento de erros
- Logging de requisições

### 5. Factory Pattern
- Criação de instâncias (ex: Reports)
- PDF vs Excel

---

## 🚀 Stack Tecnológico Recomendado

### Backend
- **Runtime:** Node.js v18+
- **Framework:** Express.js v4
- **ORM:** Sequelize v6 (ou TypeORM)
- **Database:** PostgreSQL v13+
- **Authentication:** jsonwebtoken (JWT)
- **Password Hashing:** bcryptjs
- **File Upload:** multer
- **PDF Generation:** pdfkit
- **Excel Generation:** exceljs
- **Validation:** express-validator ou joi
- **Logging:** winston ou pino
- **Environment:** dotenv

### Frontend
- **Framework:** React v18
- **Build Tool:** Vite v4
- **HTTP Client:** axios
- **State Management:** Context API ou Redux
- **UI Framework:** TailwindCSS
- **Form Handling:** react-hook-form
- **Validation:** yup ou zod
- **Date Picker:** react-datepicker
- **Notifications:** react-toastify

### DevOps
- **Version Control:** Git
- **Container:** Docker (opcional)
- **Deployment:** Heroku, Render, ou VPS
- **CI/CD:** GitHub Actions

---

## 📋 Exemplo de Requisição/Resposta

### Criar Atleta

**Request:**
```http
POST /api/atletas HTTP/1.1
Host: api.amdav.pt
Content-Type: multipart/form-data
Authorization: Bearer eyJhbGc...

{
  "nome": "João Silva",
  "data_nascimento": "1995-05-15",
  "formacao_academica": "Ensino Secundário",
  "numero_bi": "12345678",
  "telefone": "919123456",
  "tipo_deficiencia": "Mobilidade Reduzida",
  "modalidade_id": 2,
  "foto": <binary>
}
```

**Response (201 Created):**
```json
{
  "success": true,
  "message": "Atleta criado com sucesso",
  "data": {
    "id": 15,
    "nome": "João Silva",
    "data_nascimento": "1995-05-15",
    "formacao_academica": "Ensino Secundário",
    "numero_bi": "12345678",
    "telefone": "919123456",
    "tipo_deficiencia": "Mobilidade Reduzida",
    "modalidade": {
      "id": 2,
      "nome": "Atletismo"
    },
    "foto_url": "https://api.amdav.pt/uploads/fotos/15.jpg",
    "data_criacao": "2026-05-21T09:40:30Z"
  }
}
```

---

## ⚙️ Configuração de Ambiente

**Backend (.env):**
```
NODE_ENV=development
PORT=5000
DB_HOST=localhost
DB_PORT=5432
DB_NAME=amdav_db
DB_USER=postgres
DB_PASSWORD=senha123

JWT_SECRET=sua_chave_secreta_muito_segura
JWT_EXPIRY=24h

UPLOAD_DIR=./uploads
MAX_FILE_SIZE=5242880  # 5MB

SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_USER=seu_email@gmail.com
SMTP_PASS=sua_senha
```

**Frontend (.env):**
```
VITE_API_BASE_URL=http://localhost:5000/api
VITE_APP_NAME=AMDAV
```

---

## 🔄 Ciclo de Vida do Request

```
1. Cliente faz requisição HTTP
   ↓
2. Express recebe e passa por middlewares
   ├─ Parsing JSON
   ├─ CORS validation
   ├─ JWT authentication
   └─ Custom validation
   ↓
3. Route handler mapeia para controller
   ↓
4. Controller extrai dados e chama service
   ↓
5. Service executa lógica de negócio
   ├─ Validação
   ├─ Transformação de dados
   └─ Chamadas ao repository
   ↓
6. Repository interage com BD
   ├─ Query construction
   ├─ Execution
   └─ Result mapping
   ↓
7. Response percorre camadas inversamente
   ├─ Repository → Service
   ├─ Service → Controller
   └─ Controller → HTTP Response
   ↓
8. Cliente recebe resposta
```

---

## 📊 Diagrama de Componentes

```
┌─────────────────────────────────────────┐
│          FRONTEND (React)                │
│  ┌─────────────────────────────────────┐│
│  │  Pages, Components, Context, Hooks  ││
│  └────────────────┬────────────────────┘│
└────────────────┬──────────────────────────┘
                 │ HTTP/REST API
┌────────────────▼──────────────────────────┐
│          BACKEND (Express)                │
│  ┌─────────────────────────────────────┐ │
│  │  Routes → Controllers → Services    │ │
│  └────────────────┬────────────────────┘ │
│  ┌────────────────▼────────────────────┐ │
│  │  Repositories → Models              │ │
│  └────────────────┬────────────────────┘ │
└────────────────┬──────────────────────────┘
                 │ SQL/Transactions
┌────────────────▼──────────────────────────┐
│     DATABASE (PostgreSQL)                 │
│  ┌─────────────────────────────────────┐ │
│  │  Tables, Indexes, Relationships     │ │
│  └─────────────────────────────────────┘ │
└───────────────────────────────────────────┘

┌──────────────────────────────────────────┐
│    FILE STORAGE                          │
│  ┌─────────────────────────────────────┐│
│  │  /uploads/fotos                     ││
│  │  /uploads/documentos                ││
│  │  /uploads/relatorios                ││
│  └─────────────────────────────────────┘│
└──────────────────────────────────────────┘
```

---

## 🛡️ Segurança

### 1. Validação de Entrada
```javascript
// Todos os inputs validados no backend
POST /api/atletas
- Nome: trim(), minLength(3), maxLength(100), required
- Email: format email, unique
- Data: ISO format, not future date
```

### 2. Autenticação
- JWT tokens com expiração de 24h
- Refresh tokens para renovação
- Senha encriptada com bcrypt (10 rounds)

### 3. Autorização
- Middleware de roles (Admin, Gestor, Visualizador)
- Verificação de permissões por endpoint

### 4. Proteção contra Ataques
- SQL Injection: ORM + Prepared Statements
- XSS: Sanitização de inputs, React escapa automaticamente
- CSRF: CORS configuration
- Rate Limiting: Proteção contra brute force

---

## 📈 Plano de Implementação

### Fase 1 (MVP)
- [ ] Setup Backend (Express, BD)
- [ ] Autenticação JWT
- [ ] CRUD Atletas (sem relatórios)
- [ ] Setup Frontend básico
- [ ] Listagem de atletas

### Fase 2
- [ ] CRUD Direção
- [ ] CRUD Parceiros
- [ ] Filtros avançados
- [ ] Interface melhorada

### Fase 3
- [ ] Geração de Relatórios PDF
- [ ] Geração de Relatórios Excel
- [ ] Dashboard com gráficos
- [ ] Testes unitários

### Fase 4
- [ ] Melhorias UX
- [ ] Otimizações
- [ ] Deploy em produção
- [ ] Documentação API (Swagger)
