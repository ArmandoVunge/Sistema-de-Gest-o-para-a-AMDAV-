# Schema do Banco de Dados

## 📊 Diagrama de Entidades e Relacionamentos

```
┌─────────────────────┐
│     UTILIZADORES    │
├─────────────────────┤
│ id (PK)             │
│ email (UNIQUE)      │
│ username (UNIQUE)   │
│ password            │
│ perfil              │
│ ativo               │
│ data_criacao        │
│ ultima_actualizacao │
└─────────────────────┘
          │
          │ 1:N
          ▼
┌──────────────────────┐      ┌──────────────────┐
│      DIRECAO         │◄────►│    MODALIDADES   │
├──────────────────────┤      ├──────────────────┤
│ id (PK)              │      │ id (PK)          │
│ foto (blob)          │      │ nome (UNIQUE)    │
│ nome                 │      │ descricao        │
│ funcao               │      │ data_criacao     │
│ copia_bi (blob)      │      └──────────────────┘
│ telefone             │
│ contacto             │ 1:N
│ ciclo_olimpico       │◄─────┐
│ data_criacao         │      │
│ ultima_actualizacao  │      │
└──────────────────────┘      │
                              │
                    ┌─────────────────────┐
                    │      ATLETAS        │
                    ├─────────────────────┤
                    │ id (PK)             │
                    │ foto (blob)         │
                    │ nome                │
                    │ data_nascimento     │
                    │ formacao_academica  │
                    │ numero_bi           │
                    │ telefone            │
                    │ tipo_deficiencia    │
                    │ modalidade_id (FK)  │
                    │ data_criacao        │
                    │ ultima_actualizacao │
                    └─────────────────────┘

┌──────────────────────┐
│     PARCEIROS        │
├──────────────────────┤
│ id (PK)              │
│ nome                 │
│ atividade            │
│ tipo (P/T)           │
│ data_criacao         │
│ ultima_actualizacao  │
└──────────────────────┘
        │
        │ 1:N
        ▼
┌──────────────────────┐
│ CONTACTOS_PARCEIROS  │
├──────────────────────┤
│ id (PK)              │
│ parceiro_id (FK)     │
│ tipo (telefone/email)│
│ valor                │
│ data_criacao         │
└──────────────────────┘

┌──────────────────────┐
│      HISTORICO       │
├──────────────────────┤
│ id (PK)              │
│ tabela               │
│ registro_id          │
│ operacao (C/U/D)     │
│ dados_anterior       │
│ dados_novo           │
│ utilizador_id (FK)   │
│ data_operacao        │
└──────────────────────┘
```

---

## 🗄️ Scripts SQL

### Criação de Tabelas

```sql
-- Tabela de Utilizadores
CREATE TABLE utilizadores (
    id INT PRIMARY KEY AUTO_INCREMENT,
    email VARCHAR(100) UNIQUE NOT NULL,
    username VARCHAR(50) UNIQUE NOT NULL,
    password VARCHAR(255) NOT NULL,
    perfil ENUM('admin', 'gestor', 'visualizador') DEFAULT 'visualizador',
    ativo BOOLEAN DEFAULT TRUE,
    data_criacao TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    ultima_actualizacao TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);

-- Tabela de Modalidades
CREATE TABLE modalidades (
    id INT PRIMARY KEY AUTO_INCREMENT,
    nome VARCHAR(100) UNIQUE NOT NULL,
    descricao TEXT,
    data_criacao TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Tabela de Direção
CREATE TABLE direcao (
    id INT PRIMARY KEY AUTO_INCREMENT,
    foto LONGBLOB,
    nome VARCHAR(100) NOT NULL,
    funcao VARCHAR(100) NOT NULL,
    copia_bi LONGBLOB,
    telefone VARCHAR(20),
    contacto VARCHAR(100),
    ciclo_olimpico VARCHAR(50),
    data_criacao TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    ultima_actualizacao TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);

-- Tabela de Atletas
CREATE TABLE atletas (
    id INT PRIMARY KEY AUTO_INCREMENT,
    foto LONGBLOB,
    nome VARCHAR(100) NOT NULL,
    data_nascimento DATE NOT NULL,
    formacao_academica VARCHAR(255),
    numero_bi VARCHAR(20),
    telefone VARCHAR(20),
    tipo_deficiencia VARCHAR(100) NOT NULL,
    modalidade_id INT,
    data_criacao TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    ultima_actualizacao TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    FOREIGN KEY (modalidade_id) REFERENCES modalidades(id) ON DELETE SET NULL
);

-- Tabela de Parceiros
CREATE TABLE parceiros (
    id INT PRIMARY KEY AUTO_INCREMENT,
    nome VARCHAR(100) NOT NULL,
    atividade VARCHAR(255) NOT NULL,
    tipo ENUM('permanente', 'temporario') NOT NULL,
    data_criacao TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    ultima_actualizacao TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);

-- Tabela de Contactos de Parceiros
CREATE TABLE contactos_parceiros (
    id INT PRIMARY KEY AUTO_INCREMENT,
    parceiro_id INT NOT NULL,
    tipo ENUM('telefone', 'email') NOT NULL,
    valor VARCHAR(100) NOT NULL,
    data_criacao TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (parceiro_id) REFERENCES parceiros(id) ON DELETE CASCADE
);

-- Tabela de Histórico
CREATE TABLE historico (
    id INT PRIMARY KEY AUTO_INCREMENT,
    tabela VARCHAR(50) NOT NULL,
    registro_id INT NOT NULL,
    operacao ENUM('create', 'update', 'delete') NOT NULL,
    dados_anterior JSON,
    dados_novo JSON,
    utilizador_id INT,
    data_operacao TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (utilizador_id) REFERENCES utilizadores(id) ON DELETE SET NULL
);

-- Criar Índices
CREATE INDEX idx_direcao_nome ON direcao(nome);
CREATE INDEX idx_atletas_nome ON atletas(nome);
CREATE INDEX idx_atletas_modalidade ON atletas(modalidade_id);
CREATE INDEX idx_atletas_tipo_deficiencia ON atletas(tipo_deficiencia);
CREATE INDEX idx_parceiros_nome ON parceiros(nome);
CREATE INDEX idx_parceiros_tipo ON parceiros(tipo);
CREATE INDEX idx_historico_tabela ON historico(tabela);
CREATE INDEX idx_historico_data ON historico(data_operacao);
```

---

## 📋 Dicionário de Dados

### Tabela: utilizadores
| Campo | Tipo | Descrição | Restrições |
|-------|------|-----------|-----------|
| id | INT | Identificador único | PK, AUTO_INCREMENT |
| email | VARCHAR(100) | Email do utilizador | UNIQUE, NOT NULL |
| username | VARCHAR(50) | Nome de utilizador | UNIQUE, NOT NULL |
| password | VARCHAR(255) | Senha encriptada | NOT NULL |
| perfil | ENUM | Tipo de utilizador | admin/gestor/visualizador |
| ativo | BOOLEAN | Status do utilizador | DEFAULT TRUE |
| data_criacao | TIMESTAMP | Data de criação | DEFAULT NOW |
| ultima_actualizacao | TIMESTAMP | Última atualização | AUTO UPDATE |

### Tabela: atletas
| Campo | Tipo | Descrição | Restrições |
|-------|------|-----------|-----------|
| id | INT | Identificador único | PK, AUTO_INCREMENT |
| foto | LONGBLOB | Foto do atleta | OPTIONAL |
| nome | VARCHAR(100) | Nome completo | NOT NULL |
| data_nascimento | DATE | Data de nascimento | NOT NULL |
| formacao_academica | VARCHAR(255) | Nível académico | OPTIONAL |
| numero_bi | VARCHAR(20) | Número de BI | OPTIONAL |
| telefone | VARCHAR(20) | Contacto telefónico | OPTIONAL |
| tipo_deficiência | VARCHAR(100) | Tipo de deficiência | NOT NULL |
| modalidade_id | INT | ID da modalidade | FK |
| data_criacao | TIMESTAMP | Data de criação | DEFAULT NOW |
| ultima_actualizacao | TIMESTAMP | Última atualização | AUTO UPDATE |

### Tabela: direcao
| Campo | Tipo | Descrição | Restrições |
|-------|------|-----------|-----------|
| id | INT | Identificador único | PK, AUTO_INCREMENT |
| foto | LONGBLOB | Foto do membro | OPTIONAL |
| nome | VARCHAR(100) | Nome completo | NOT NULL |
| funcao | VARCHAR(100) | Função na direção | NOT NULL |
| copia_bi | LONGBLOB | Cópia do BI | OPTIONAL |
| telefone | VARCHAR(20) | Contacto telefónico | OPTIONAL |
| contacto | VARCHAR(100) | Contacto adicional | OPTIONAL |
| ciclo_olimpico | VARCHAR(50) | Ciclo olímpico | OPTIONAL |
| data_criacao | TIMESTAMP | Data de criação | DEFAULT NOW |
| ultima_actualizacao | TIMESTAMP | Última atualização | AUTO UPDATE |

### Tabela: parceiros
| Campo | Tipo | Descrição | Restrições |
|-------|------|-----------|-----------|
| id | INT | Identificador único | PK, AUTO_INCREMENT |
| nome | VARCHAR(100) | Nome do parceiro | NOT NULL |
| atividade | VARCHAR(255) | Atividade desenvolvida | NOT NULL |
| tipo | ENUM | Tipo (permanente/temporário) | NOT NULL |
| data_criacao | TIMESTAMP | Data de criação | DEFAULT NOW |
| ultima_actualizacao | TIMESTAMP | Última atualização | AUTO UPDATE |
