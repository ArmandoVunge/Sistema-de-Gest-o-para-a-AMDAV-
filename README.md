# Sistema de Gestão AMDAV

Desportos Adaptados nos Municípios - Sistema de Gestão para a Associação Municipal dos Desportos Adaptados de Viana (AMDAV)

## 📋 Funcionalidades

### 1. Direção
Gestão dos membros da direção da associação.

**Campos de Cadastro:**
- Foto
- Nome
- Função
- Cópia do BI
- Telefone
- Contacto
- Ciclo Olímpico

**Operações:** Cadastrar, Editar, Listar, Eliminar

---

### 2. Atletas
Gestão dos atletas da associação com relatórios detalhados.

**Campos de Cadastro:**
- Foto
- Nome
- Data de Nascimento
- Formação Académica
- Número do BI
- Telefone
- Tipo de Deficiência
- Modalidade

**Funcionalidades:**
- Cadastrar atleta
- Editar informações
- Listar atletas por modalidade
- Gerar relatórios (PDF/Excel)
- Filtrar por tipo de deficiência, modalidade, etc.

---

### 3. Parceiros
Gestão de parceiros da associação.

**Campos de Cadastro:**
- Nome do Parceiro
- Atividade que Desenvolve
- Tipo (Permanente/Temporário)
- Contactos

**Operações:** Cadastrar, Editar, Listar, Eliminar

---

## 🛠️ Tecnologias (A Definir)

- Backend: [Node.js/Python/Django]
- Frontend: [React/Vue/HTML/CSS]
- Database: [PostgreSQL/MySQL/MongoDB]
- Relatórios: [PDF - PDFKit, Excel - OpenPyXL/ExcelJS]

---

## 📁 Estrutura do Projeto

```
Sistema-de-Gest-o-para-a-AMDAV-/
├── README.md
├── docs/
│   ├── REQUISITOS.md
│   ├── ARQUITETURA.md
│   └── BANCO_DADOS.md
├── backend/
│   ├── models/
│   │   ├── direcao.model.js
│   │   ├── atleta.model.js
│   │   └── parceiro.model.js
│   ├── routes/
│   │   ├── direcao.routes.js
│   │   ├── atleta.routes.js
│   │   └── parceiro.routes.js
│   ├── controllers/
│   │   ├── direcao.controller.js
│   │   ├── atleta.controller.js
│   │   └── parceiro.controller.js
│   └── app.js
├── frontend/
│   ├── components/
│   │   ├── Direcao/
│   │   ├── Atletas/
│   │   └── Parceiros/
│   ├── pages/
│   ├── assets/
│   └── index.html
└── database/
    └── schema.sql
```

---

## 🚀 Próximos Passos

1. Definir tecnologias (backend, frontend, banco de dados)
2. Criar documentação detalhada do banco de dados
3. Implementar autenticação e autorização
4. Desenvolver módulos (Direção, Atletas, Parceiros)
5. Implementar geração de relatórios (PDF/Excel)
6. Testes e validações

---

## 📝 Licença

A definir

## 👤 Autor

ArmandoVunge
