# Especificação Funcional e Regras de Negócio - SGP

## 1. Introdução
O **SGP (Sistema de Gestão de Problemas)** é uma plataforma de ITSM focada na gestão integrada de Incidentes, Problemas e Base de Conhecimento. O sistema visa operacionalizar processos ITIL para reduzir o tempo de inatividade de serviços e prevenir recorrências de falhas.

**Premissas do Projeto:**
- **Idioma**: Interface e dados padrão totalmente em **Português do Brasil (pt-BR)**.
- **Segurança**: Arquitetura robusta com foco em ACL (Access Control List), validação de dados e proteção contra vulnerabilidades web comuns.
- **Stack**: Laravel 12, FilamentPHP, Livewire, TailwindCSS, Banco de Dados Relacional (MySQL/PostgreSQL).

---

## 2. Requisitos Não Funcionais Críticos

### 2.1 Segurança e Controle de Acesso (ACL)
- **Granularidade de Permissões**: O sistema deve implementar um controle de acesso baseado em papéis (RBAC) rigoroso.
- **Autenticação**: Suporte a autenticação segura (padrão Laravel), com preparação para integração futura (LDAP/SSO).
- **Auditoria**:
    - Todo registro (criação, edição, exclusão) deve ter log de auditoria (Quem, Quando, O Quê).
    - Histórico de alterações de status em tickets é imutável.
- **Proteção de Dados**:
    - Sanitização de inputs para prevenir XSS e SQL Injection.
    - CSRF Protection habilitado em todos os formulários.
    - Rate Limiting em rotas críticas (login, criação de tickets pública) para evitar flood/DDoS.

### 2.2 Desempenho e Usabilidade
- **Tempo de Resposta**: Operações de CRUD devem responder em < 500ms.
- **Busca**: Mecanismo de busca eficiente para a Base de Conhecimento e Tickets.
- **Interface**: Responsiva (Desktop/Mobile), com Tema Escuro/Claro (Dark Mode support do Filament).

---

## 3. Features Principais

### 3.1 Módulo de Gestão de Incidentes
**Objetivo**: Restaurar a operação normal do serviço o mais rápido possível.

- **Registro de Incidentes**:
    - Criação via interface interna (Service Desk).
    - Campos: Título, Descrição, Categoria, Prioridade (Matriz Impacto x Urgência), Solicitante, Atribuído a.
- **Fluxo de Trabalho**:
    - Estados: `Novo` -> `Em Análise` -> `Em Progresso` -> `Pendente` -> `Resolvido` -> `Fechado` -> `Cancelado`.
- **SLA (Service Level Agreement)**:
    - Definição de prazo de resolução baseado na Prioridade.
    - Indicador visual de vencimento (SLA Timer).
- **Vínculos**:
    - Associação com *Problemas* existentes.
    - Associação com *Artigos de Conhecimento* usados na solução.

### 3.2 Módulo de Gestão de Problemas
**Objetivo**: Identificar e remover a causa raiz de incidentes.

- **Registro de Problemas**:
    - Criação manual ou a partir de um Incidente.
    - Campos: Causa Raiz, Solução de Contorno (Workaround), Solução Definitiva.
- **BDEC (Base de Dados de Erros Conhecidos)**:
    - Marcar problema como "Erro Conhecido".
    - Disponibilizar Workaround automaticamente para técnicos de Incidentes.
- **Fluxo de Trabalho**:
    - Estados: `Novo` -> `Em Investigação` -> `Causa Raiz Identificada` -> `Solução Definida` -> `Resolvido` -> `Fechado`.

### 3.3 Módulo Base de Conhecimento (KB)
**Objetivo**: Armazenar, compartilhar e gerenciar conhecimento organizacional.

- **Gestão de Artigos**:
    - Editor Rich-Text (Markdown/WYSIWYG).
    - Categorização hierárquica.
    - Tags para busca.
- **Ciclo de Vida**:
    - `Rascunho` -> `Revisão` -> `Publicado` -> `Arquivado`.
- **Integração**:
    - Sugestão de artigos na tela de criação de Incidentes.

---

## 4. Regras de Negócio (RN)

### RN01 - Matriz de Prioridade
A prioridade de um Incidente é calculada automaticamente:
- **Impacto** (Alto, Médio, Baixo) x **Urgência** (Alta, Média, Baixa).
- Exemplo: Impacto Alto + Urgência Alta = Prioridade **Crítica**.

### RN02 - Fechamento de Incidentes Vinculados
- Quando um **Problema** é marcado como `Resolvido` ou `Fechado`, o sistema deve notificar os responsáveis pelos **Incidentes** vinculados.
- Opção para "Resolução em Lote": O técnico pode optar por resolver todos os incidentes filhos aplicando a Solução Definitiva do Problema.

### RN03 - Visibilidade da Base de Conhecimento
- Artigos marcados como "Interno" são visíveis apenas para perfis `Técnico` e `Gestor`.
- Artigos "Públicos" (futuro) poderiam ser vistos por `Solicitantes`.
- Workarounds de Erros Conhecidos são visíveis imediatamente na tela de Incidentes.

### RN04 - Imutabilidade de Auditoria
- Comentários e alterações de status não podem ser excluídos permanentemente (Soft Delete) para garantir rastreabilidade.

### RN05 - Atribuição Automática (Opcional Fase 1)
- Incidentes podem ser atribuídos a grupos de técnicos baseados na **Categoria** do incidente (ex: Categoria "Rede" -> Grupo "Infraestrutura").

---

## 5. Perfis de Acesso e Permissões (ACL)

O sistema utilizará **Filament Shield** ou políticas nativas do Laravel para gerenciar as seguintes roles:

### 5.1 Admin (Super Admin)
- Acesso total ao sistema.
- Gerenciamento de Usuários, Roles e Permissões.
- Configuração de Tabelas Auxiliares (Categorias, Serviços, SLAs).

### 5.2 Gestor (Problem Manager / Service Desk Lead)
- **Incidentes**: Ver todos, escalar, reatribuir, deletar (soft delete).
- **Problemas**: Criação, Gestão completa, Fechamento.
- **KB**: Publicação e Aprovação de artigos.
- **Relatórios**: Acesso total a Dashboards e Métricas.

### 5.3 Técnico (Analista N1/N2)
- **Incidentes**: Criar, Editar (apenas os seus ou de seu grupo), Resolver.
- **Problemas**: Visualizar, Sugerir criação, Vincular incidentes.
- **KB**: Visualizar, Criar Rascunhos, Sugerir edições.
- **Acesso Restrito**: Não pode configurar sistema nem ver relatórios gerenciais globais.

### 5.4 Solicitante (Basic User - Futuro)
- Apenas visualizar seus próprios tickets.
- Abrir novos incidentes via portal simplificado.
