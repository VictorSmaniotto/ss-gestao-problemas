# Refinamento Inicial - SGP (Sistema de Gestão de Problemas)

## Resumo do Problema
O cliente deseja desenvolver uma plataforma unificada de ITSM baseada em ITIL para gerenciar Incidentes, Problemas e Base de Conhecimento, visando reduzir o tempo de recuperação de serviços e eliminar causas raiz de falhas recorrentes. O sistema deve atender equipes técnicas e de gestão com interfaces distintas, suportar fluxos de trabalho integrados e fornecer métricas de desempenho (KPIs). Atualmente, a falta de integração entre esses processos gera ineficiência e retrabalho operacional nas equipes de suporte.

## Perguntas Estruturadas

### Regras de Negócio
- Qual é a matriz exata de Prioridade (Impacto x Urgência) que deve ser implementada? Existem prazos padrão de SLA definidos para cada combinação?
- Como deve se comportar o sistema ao tentar fechar um Problema que ainda possui Incidentes abertos vinculados? Deve bloquear, fechar em cascata ou apenas alertar?
- Na Base de Conhecimento, qual é o fluxo de aprovação de um artigo? Qualquer técnico pode publicar ou é necessário um perfil de "Revisor"?
- Quais são os critérios automáticos para sugerir que um Incidente seja promovido a Problema? (Ex: X incidentes similares em Y dias?)
- A "solução de contorno" (workaround) deve ser visível para o usuário final no portal de autoatendimento ou apenas para técnicos?

### Fluxos Operacionais
- No fluxo de Incidentes, o escalonamento para Nível 2 transfere a propriedade do ticket ou mantém a responsabilidade compartilhada?
- O fechamento de um Incidente exige validação explícita do usuário requerente? Se o usuário não responder, o sistema encerra automaticamente após quanto tempo?
- Como funciona o versionamento de artigos na Base de Conhecimento? Mantemos histórico de alterações para auditoria?

### Exceções
- O que acontece se um incidente crítico for aberto fora do horário de expediente? O sistema deve acionar algum plantão (via SMS/Phone) ou apenas notificar via e-mail?
- É permitido reabrir um Incidente ou Problema fechado? Se sim, qual o prazo limite para essa ação?
- Se um Problema for considerado "Sem Solução" (ex: limitação tecnológica), como ficam os Incidentes vinculados? Eles são fechados com qual justificativa?

### Parametrização / Portfólio / Ofertas
- O Catálogo de Serviços será importado de alguma fonte externa ou cadastrado manualmente? Quais atributos mínimos um Serviço deve ter?
- As categorias de incidentes podem ter quantos níveis de hierarquia (ex: Hardware > Periféricos > Mouse)?
- Os SLAs são configurados por Serviço, por Categoria ou por Prioridade Global? Qual a precedência se houver conflito?

### Financeiro / Contábil / Conciliação
- *Não identificado impacto financeiro direto/faturamento no escopo atual.*

### Atendimento / Suporte
- O sistema deve permitir chat em tempo real entre solicitante e técnico, ou a comunicação é assíncrona via comentários no ticket?
- Existe necessidade de pesquisa de satisfação (CSAT) automática após o fechamento de cada incidente?

### Integrações
- Já existe algum provedor de identidade (AD, LDAP, OIDC) definido para a autenticação dos usuários, ou o sistema gerenciará credenciais localmente?
- O sistema precisa integrar com ferramentas de monitoramento (Zabbix, Prometheus, Datadog) para abertura automática de incidentes na Fase 1?
- Há necessidade de envio de mensagens para Slack/Teams/WhatsApp, ou apenas e-mail é suficiente para notificações?

### Dúvidas Gerais
- O documento menciona "Suporte a múltiplos idiomas no futuro", mas o requisito atual é PT-BR. A estrutura de banco deve nascer pronta para i18n?
- Qual é a expectativa de volume de dados (tickets/mês) para dimensionamento de banco e armazenamento de anexos?

## Assunções a Validar
- Assumo que o sistema será Multi-Tenant ou suportará segregação lógica de dados, visto que pode haver departamentos com dados sensíveis (RH, Jurídico).
- Assumo que a gestão de usuários e perfis (ACL) será granular, permitindo criar novos perfis além dos padrões (Técnico, Gestor, Admin).
- Assumo que o sistema deve rodar em ambiente Dockerizado para facilitar deploy, conforme mencionado nas boas práticas de arquitetura.
- Assumo que o envio de e-mails transacionais (abertura, atualização, fechamento) é requisito obrigatório desde o MVP.

## Riscos Identificados
- **Técnico**: A implementação de uma busca textual eficiente (Full-text search) para a Base de Conhecimento pode exigir recursos adicionais de infraestrutura (ex: ElasticSearch), aumentando a complexidade do deploy.
- **Operacional**: A falta de definição clara dos processos de ITIL na organização pode levar a solicitações frequentes de mudança nos fluxos do sistema durante o desenvolvimento.
- **Negócio**: Se a cultura de documentação não for incentivada, a Base de Conhecimento pode ficar vazia ou desatualizada, reduzindo o valor entregue pela ferramenta (risco de adoção).
- **Segurança**: A integração entre módulos (Incidente <-> Problema) se não tiver ACL rigoroso pode expor dados sensíveis de um problema raiz para técnicos de Nível 1 que não deveriam ter acesso.

## Pontos para VOC (Voice of Customer)
- Validar a *matriz de prioridade e SLA*: Isso define o "coração" das regras de negócio de tempo.
- Definir o *fluxo de aprovação de conhecimento*: Isso impacta diretamente na qualidade da base e na governança.
- Confirmar a *estratégia de autenticação* (Local vs Integrada): Impacta profundamente a segurança e o setup inicial.
- Validar a *necessidade de canais de notificação* além de e-mail (Push, Chat): Define escopo de integrações externas.
