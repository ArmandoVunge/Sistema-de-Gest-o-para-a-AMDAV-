# Requisitos do Sistema

## 🎯 Requisitos Funcionais (RF)

### Módulo 1: Direção

#### RF1.1 - Cadastro de Membro da Direção
- **Descrição:** Permitir o cadastro de novos membros da direção
- **Atores:** Gestor, Admin
- **Campos Obrigatórios:** Nome, Função
- **Campos Opcionais:** Foto, Cópia do BI, Telefone, Contacto, Ciclo Olímpico
- **Fluxo Principal:**
  1. Utilizador acede ao formulário de cadastro
  2. Preence os dados do membro
  3. Faz upload de foto (opcional)
  4. Faz upload de cópia do BI (opcional)
  5. Submete o formulário
  6. Sistema valida e guarda na BD
  7. Confirmação de sucesso

#### RF1.2 - Editar Membro da Direção
- **Descrição:** Permitir edição dos dados de um membro existente
- **Atores:** Gestor, Admin
- **Campos Editáveis:** Todos

#### RF1.3 - Listar Membros da Direção
- **Descrição:** Visualizar lista de todos os membros com paginação
- **Atores:** Todos
- **Filtros:** Por Função, Por Ciclo Olímpico

#### RF1.4 - Eliminar Membro da Direção
- **Descrição:** Remover um membro da base de dados
- **Atores:** Admin
- **Validação:** Confirmar eliminação

---

### Módulo 2: Atletas

#### RF2.1 - Cadastro de Atleta
- **Descrição:** Permitir o cadastro de novos atletas
- **Atores:** Gestor, Admin
- **Campos Obrigatórios:** Nome, Data de Nascimento, Tipo de Deficiência, Modalidade
- **Campos Opcionais:** Foto, Formação Académica, Número do BI, Telefone
- **Fluxo Principal:**
  1. Utilizador acede ao formulário de cadastro
  2. Preece dados do atleta
  3. Seleciona modalidade (dropdown da lista)
  4. Faz upload de foto (opcional)
  5. Submete formulário
  6. Sistema valida e guarda
  7. Confirmação de sucesso

#### RF2.2 - Editar Informações do Atleta
- **Descrição:** Permitir edição dos dados de um atleta
- **Atores:** Gestor, Admin
- **Campos Editáveis:** Todos

#### RF2.3 - Listar Atletas por Modalidade
- **Descrição:** Visualizar lista de atletas agrupados por modalidade
- **Atores:** Todos
- **Exibição:**
  - Agrupar por modalidade
  - Mostrar foto, nome, tipo de deficiência
  - Paginação
  - Filtros por modalidade, tipo de deficiência

#### RF2.4 - Gerar Relatório em PDF
- **Descrição:** Exportar dados dos atletas em PDF
- **Atores:** Gestor, Admin
- **Opções:**
  - Todos os atletas
  - Por modalidade específica
  - Por tipo de deficiência
  - Incluir/Excluir fotos

#### RF2.5 - Gerar Relatório em Excel
- **Descrição:** Exportar dados dos atletas em Excel
- **Atores:** Gestor, Admin
- **Opções:** Similares ao PDF

#### RF2.6 - Eliminar Atleta
- **Descrição:** Remover um atleta da base de dados
- **Atores:** Admin
- **Validação:** Confirmar eliminação

---

### Módulo 3: Parceiros

#### RF3.1 - Cadastro de Parceiro
- **Descrição:** Permitir o cadastro de novos parceiros
- **Atores:** Gestor, Admin
- **Campos Obrigatórios:** Nome, Atividade, Tipo
- **Campos Opcionais:** Contactos
- **Fluxo Principal:**
  1. Utilizador acede ao formulário
  2. Preence dados do parceiro
  3. Seleciona tipo (Permanente/Temporário)
  4. Adiciona contactos (telefone/email)
  5. Submete formulário
  6. Sistema valida e guarda
  7. Confirmação de sucesso

#### RF3.2 - Editar Parceiro
- **Descrição:** Permitir edição dos dados de um parceiro
- **Atores:** Gestor, Admin
- **Campos Editáveis:** Todos

#### RF3.3 - Listar Parceiros
- **Descrição:** Visualizar lista de todos os parceiros
- **Atores:** Todos
- **Filtros:** Por Tipo (Permanente/Temporário)

#### RF3.4 - Eliminar Parceiro
- **Descrição:** Remover um parceiro
- **Atores:** Admin
- **Validação:** Confirmar eliminação

---

### Módulo Transversal: Autenticação

#### RF4.1 - Login
- **Descrição:** Autenticar utilizador no sistema
- **Atores:** Todos
- **Campos:** Email/Username e Password
- **Validação:** Verificar credenciais na BD

#### RF4.2 - Logout
- **Descrição:** Terminar sessão
- **Atores:** Todos

#### RF4.3 - Gestão de Perfis
- **Descrição:** Controlar permissões por perfil
- **Perfis:**
  - **Admin:** Acesso total, pode eliminar, criar utilizadores
  - **Gestor:** Pode criar, editar, listar, gerar relatórios
  - **Visualizador:** Apenas pode consultar/listar

---

## 🏗️ Requisitos Não-Funcionais (RNF)

### RNF1 - Performance
- Tempo de resposta < 2 segundos para operações comuns
- Carregar listagens com até 1000 registos em < 3 segundos
- Relatórios gerados em < 5 segundos

### RNF2 - Segurança
- Encriptação de senhas com bcrypt
- Validação de entrada em todos os formulários
- Proteção contra SQL Injection
- Autenticação JWT com tokens de curta duração
- Logs de auditoria para operações críticas

### RNF3 - Disponibilidade
- Sistema disponível 24/7
- Backup automático diário do banco de dados
- Recuperação de dados em caso de falha

### RNF4 - Usabilidade
- Interface intuitiva e responsiva
- Suporte para dispositivos móveis
- Mensagens de erro claras em português
- Navegação clara e consistente

### RNF5 - Manutenibilidade
- Código estruturado seguindo padrões MVC
- Documentação completa do código
- Testes unitários com cobertura > 80%

### RNF6 - Escalabilidade
- Arquitetura preparada para crescimento
- Índices na BD para otimização
- Possibilidade de adicionar novos módulos

---

## ✅ Critérios de Aceitação

### Cadastro de Atleta
- [ ] Formulário apresenta todos os campos especificados
- [ ] Validação de campos obrigatórios
- [ ] Upload de foto funciona correctamente
- [ ] Modalidade é selecionada de dropdown
- [ ] Dados são guardados na BD corretamente
- [ ] Mensagem de sucesso é apresentada
- [ ] Pode-se editar atleta após criação
- [ ] Foto é armazenada e recuperada sem perda de qualidade

### Geração de Relatório PDF
- [ ] Botão "Gerar PDF" está visível
- [ ] Pode filtrar por modalidade antes de gerar
- [ ] PDF é gerado correctamente
- [ ] Contém todos os dados do atleta
- [ ] Formatação está apresentável
- [ ] Pode incluir/excluir fotos
- [ ] Download funciona correctamente

### Geração de Relatório Excel
- [ ] Botão "Gerar Excel" está visível
- [ ] Pode filtrar por modalidade
- [ ] Arquivo .xlsx é gerado
- [ ] Contém todos os dados do atleta
- [ ] Colunas estão bem organizadas
- [ ] Download funciona correctamente

### Listagem por Modalidade
- [ ] Atletas são agrupados correctamente
- [ ] Cada grupo mostra foto e nome
- [ ] Paginação funciona
- [ ] Filtros funcionam correctamente
- [ ] Contagem de atletas por modalidade está visível

---

## 📊 Histórias de Utilizador

### HU1 - Como Gestor, quero cadastrar atletas rapidamente
```gherkin
Cenário: Cadastro bem-sucedido de atleta
  Dado que estou na página de cadastro de atletas
  E preço os dados obrigatórios (nome, data nascimento, deficiência, modalidade)
  Quando clico em "Guardar"
  Então o atleta é guardado na BD
  E recebo confirmação de sucesso
  E o formulário é limpo para novo cadastro
```

### HU2 - Como Admin, quero gerar relatórios dos atletas
```gherkin
Cenário: Gerar relatório em PDF
  Dado que estou na listagem de atletas
  E quero exportar dados para PDF
  Quando clico em "Exportar PDF"
  Então é gerado um arquivo PDF
  E é iniciado o download automático
```

---

## 🎮 Casos de Uso Principais

```
┌─────────────────────────────────────────────────────────┐
│              CASOS DE USO DO SISTEMA                    │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  ┌──────────────┐          ┌──────────────┐            │
│  │   Gestor     │          │    Admin     │            │
│  └──────────────┘          └──────────────┘            │
│        │                          │                    │
│        │────┐                 ┌───┤                    │
│        │    │                 │   │                    │
│        ├─ Cadastrar Atleta    │   ├─ Gerir Utilizadores
│        ├─ Editar Atleta       │   ├─ Eliminar Registos
│        ├─ Cadastrar Direção   │   └─ Ver Auditoria
│        ├─ Cadastrar Parceiro  │
│        ├─ Gerar Relatórios    │
│        └─ Listar Registos     │
│                               │
│         ┌────────────────────────┐
│         │  Todos os Utilizadores │
│         ├────────────────────────┤
│         └─ Login/Logout
│         └─ Visualizar Dados
│
└─────────────────────────────────────────────────────────┘
```

---

## 🔄 Fluxo de Autenticação

```
Usuario não autenticado
        │
        ├─► Submete Email + Password
        │
        ├─► Sistema valida credenciais
        │   - Verifica se existe em BD
        │   - Verifica se password está correcta
        │
        ├─ Se inválido ──► Erro: Credenciais inválidas
        │
        ├─ Se válido ────► Gera JWT Token
        │                 ├─ Token contém ID do utilizador
        │                 ├─ Token contém Perfil
        │                 └─ Token válido por 24h
        │
        ├─► Armazena token no browser
        │
        └─► Redireciona para Dashboard
            ├─ Request sempre inclui token no header
            ├─ Se token inválido ──► Redireciona para Login
            └─ Se token válido ────► Carrega página
```
