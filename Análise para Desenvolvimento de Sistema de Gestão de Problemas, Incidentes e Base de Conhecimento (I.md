

Análise para Desenvolvimento de Sistema de
Gestão de Problemas, Incidentes e Base de
Conhecimento (ITIL)
## Introdução
Este relatório apresenta uma análise detalhada para orientar o desenvolvimento de um software de
gestão de problemas, gestão de incidentes e base de conhecimento alinhado às boas práticas do
ITIL. O objetivo é fornecer às equipes de suporte técnico, product owners e time técnico uma
plataforma unificada para registrar e solucionar incidentes rapidamente, investigar e resolver causas
raiz de problemas e compartilhar conhecimento de forma reutilizável. A seguir, são descritas as
funcionalidades essenciais do sistema, os fluxos de trabalho principais (com ênfase na integração entre
a gestão de problemas e de incidentes), os requisitos funcionais e não funcionais, a arquitetura técnica
recomendada, a interface esperada para diferentes perfis de usuário e os indicadores-chave com seus
painéis de monitoramento.
- Funcionalidades Essenciais do Sistema
O sistema proposto deverá abranger três módulos integrados:  Gestão de Problemas,   Gestão de
Incidentes e  Base de Conhecimento. A integração entre esses módulos garantirá que informações de
erros conhecidos e soluções sejam compartilhadas, agilizando a resolução de incidentes e prevenindo
recorrências. Abaixo detalhamos as funcionalidades essenciais de cada módulo, de acordo com
o processo ITIL e referência do IFTO:
1.1 Funcionalidades de Gestão de Problemas
Detecção de Problemas: Possibilidade de identificar problemas de forma reativa (a partir de
um ou mais incidentes relacionados, análise de impactos ou alertas de eventos) ou proativa (via
análise de tendências de incidentes e identificação de riscos antes que causem falhas). O
sistema deve permitir registrar suspeitas de problema oriundas do Service Desk, equipes
técnicas ou ferramentas de monitoramento.
Registro do Problema: Criação de um registro formal de problema no sistema, contendo
detalhes mínimos como descrição, sintomas, mensagem de erro, serviço afetado, histórico de
recorrência e incidentes relacionados. Mesmo após um incidente ser resolvido, pode-se
registrar um problema para investigação adicional de causa raiz. Cada problema recebe um
identificador único e data/hora de registro para rastreabilidade.
Categorização do Problema: Classificação do problema por tipo (ex.: rede, aplicação, hardware)
e serviço afetado. A categorização deve seguir o mesmo esquema usado em incidentes para
manter consistência. De acordo com a categoria, o sistema pode sugerir automaticamente
qual grupo técnico ou especialista deve ser responsável pela investigação. Essa
funcionalidade ajuda a identificar padrões de problemas em áreas específicas e facilita análises
posteriores.
Priorização do Problema: Definição da prioridade com base em urgência e impacto, através
de uma matriz de prioridade (impacto nos negócios versus tempo de resposta necessário).
## 12
## •
## 34
## •
## 56
## 7
## 8
## •
## 9
## 10
## •
## 11
## 1

Problemas que causam alto impacto ou representam risco de incidentes graves devem ser
marcados como alta prioridade. Essa ordenação garante que problemas críticos sejam tratados
primeiro, organizando a carga de trabalho de acordo com o risco ao negócio.
Investigação e Diagnóstico: Ferramentas para a equipe técnica realizar análise da causa raiz
do problema. O sistema deve permitir registrar evidências, hipóteses e resultados de
diagnósticos (análise de logs, 5 Porquês, etc.). É nessa etapa que se aprofunda o estudo do
problema para identificar o motivo fundamental da falha. A plataforma deve facilitar a
colaboração entre especialistas, incluindo histórico de ações investigativas e anexos (como logs
ou relatórios) relevantes.
Erro Conhecido e Solução de Contorno: Caso a causa raiz seja identificada ou uma solução
temporária (workaround) seja encontrada, o problema deve ser marcado como Erro
Conhecido e registrado na Base de Dados de Erros Conhecidos (BDEC). A BDEC é um
repositório dentro da base de conhecimento para documentar problemas já analisados com
suas soluções de contorno ou definitivas. O sistema deve permitir associar ao registro do
problema a descrição da solução de contorno (workaround) aprovada, para que equipes de
suporte possam consultá-la rapidamente em novos incidentes semelhantes. Ex: “Erro
Conhecido” indica que o problema já tem causa raiz conhecida e pelo menos uma mitigação
documentada.
Solução Definitiva do Problema: Uma vez desenvolvida uma solução permanente, a equipe
de problemas registra a resolução definitiva no sistema. Em muitos casos, a solução envolverá
implementar uma mudança na infraestrutura ou software – o sistema deve então gerar ou
integrar-se a uma Requisição de Mudança (RDM) para gestão de mudanças, garantindo
implementação controlada da correção. Se a solução puder ser aplicada imediatamente
sem necessidade de mudança formal, o registro deve permitir marcar a ação de correção direta
realizada. Todas as ações de solução devem ser documentadas.
Fechamento do Problema: Encerramento formal do registro de problema após verificação de
que a solução definitiva foi aplicada com sucesso. Nesta etapa, o sistema deve solicitar
validações, incluindo: confirmação de que todos os incidentes associados foram resolvidos/
fechados, e que as informações do problema (causa, solução) foram devidamente registradas
na base de conhecimento/BDEC. O status do problema é atualizado para concluído e ele
é marcado como resolvido. É recomendável que o fechamento inclua uma revisão final,
anexando “lições aprendidas” ou notas de prevenção para futuro, principalmente se foi um
problema grave (alta severidade).
(Obs.: Os subprocessos do gerenciamento de problemas conforme ITIL incluem detectar, registrar, categorizar,
priorizar, aplicar workaround, investigar/diagnosticar, consultar/registrar erro conhecido, resolver e fechar o
problema. O sistema deve suportar todos esses estágios para cobrir o ciclo de vida completo de um
problema.)
1.2 Funcionalidades de Gestão de Incidentes
Registro e Categorização de Incidentes: Permite que qualquer incidente (interrupção ou
degradação de um serviço de TI) seja registrado no sistema de forma consistente, contendo
data/hora, descrição do sintoma, usuário afetado, serviço ou item de configuração afetado, etc.
. Ao registrar, o atendente deve categorizar o incidente (por tipo de problema, área
responsável, urgência/impacto) e, se possível, já atribuir uma prioridade inicial. A
categorização adequada é essencial para encaminhar o incidente ao grupo de suporte correto e
identificar incidentes recorrentes no futuro. O sistema também deve permitir registro de
incidentes via múltiplos canais (portal web, e-mail, telefone via um agente registrando),
unificando todos em uma mesma base de dados de chamados.
## 12
## •
## 13
## •
## 142
## 15
## 162
## 17
## •
## 1819
## 2021
## •
## 2223
## 2425
## 2627
## •
## 2829
## 11
## 29
## 2

Prioridade e Roteamento: Com base na categorização e em regras de negócios (matriz de
impacto × urgência), o sistema define ou sugere a prioridade do incidente (ex.: Crítico, Alto,
Médio, Baixo). Incidentes críticos ou que afetam muitos usuários devem ser sinalizados. O
incidente então é atribuído automaticamente ou manualmente a um técnico ou grupo de
suporte apropriado (Nível 1, 2, ou especialista), de acordo com a categoria e prioridade. Regras
de escalonamento devem existir: se o incidente não for resolvido em determinado tempo ou
exigir conhecimento especializado, o sistema deve facilitar sua transferência para o próximo
nível de suporte ou notificar gestores responsáveis.
Investigação e Diagnóstico Inicial: Ferramentas para que a equipe de suporte realize o
diagnóstico do incidente. O técnico pode consultar diretamente a Base de Conhecimento em
busca de soluções conhecidas – por exemplo, verificar na BDEC se já há um erro conhecido e
workaround para os sintomas relatados. Se existir uma solução documentada para incidente
semelhante, ela pode ser aplicada imediatamente, agilizando a resolução. Caso
contrário, o técnico segue procedimentos de análise: coletar logs, reproduzir o problema, fazer
perguntas ao usuário, etc., tudo registrando as atividades e notas no ticket. O sistema deve
permitir anexos (prints de erro, arquivos de log) e comentários colaborativos.
Resolução e Recuperação do Serviço: Uma vez encontrada uma solução (temporária ou
definitiva) que restaure o serviço, o técnico registra a resolução do incidente no sistema. O
status do incidente é atualizado para Resolvido ou Recuperado, e o serviço é restaurado ao
funcionamento normal. É importante que o sistema capture o que causou o incidente e
quais ações foram tomadas para resolvê-lo, seja na forma de campos estruturados (categoria
de causa raiz conhecida, por exemplo) ou descrição textual. Se a resolução for um
workaround temporário aplicado à espera de uma correção permanente via gerenciamento de
problemas, isso deve estar indicado no chamado (e idealmente ligado a um registro de
problema correspondente).
Fechamento e Validação: O incidente pode ser fechado pelo Service Desk após confirmar-se
que a solução restaurou o serviço e que o usuário afetado concorda que o incidente foi resolvido
(quando aplicável). No fechamento, o sistema solicita a documentação final: confirmação
da causa (se conhecida), solução aplicada e referência a algum artigo de base de conhecimento
utilizado ou criado. Esses dados alimentam relatórios e a melhoria contínua do processo de
incidentes. Incidentes vinculados a um problema conhecido também podem ser fechados
em lote quando o problema for resolvido definitivamente – o sistema deve suportar esse
fechamento múltiplo vinculado. Após fechamento, nenhuma edição no chamado deve ser
permitida (somente reabertura, se o usuário reportar recorrência).
(Obs.: O processo de gestão de incidentes ITIL em linhas gerais inclui identificar/detectar o incidente, registrar
e categorizar, realizar diagnóstico inicial, priorizar, escalonar se necessário, investigar e resolver, restaurar o
serviço e fechar/documentar o incidente. Todas essas etapas devem ser suportadas pelo software. Um
benefício de seguir esse fluxo estruturado é restaurar serviços mais rapidamente e capturar dados valiosos
para prevenção de problemas futuros.)
1.3 Funcionalidades da Base de Conhecimento (Knowledge Base)
BDEC – Base de Dados de Erros Conhecidos: O sistema deve incluir uma BDEC, que é a porção
da base de conhecimento dedicada a erros conhecidos (problemas já diagnosticados com causa
raiz e workaround ou solução documentada). Cada registro na BDEC deve armazenar o
descritor do problema, sintomas, causa raiz confirmada, solução de contorno aprovada e,
quando disponível, a solução definitiva. A BDEC é parte integrante do conhecimento
organizacional de TI, permitindo que a equipe de incidentes encontre rapidamente se um novo
incidente corresponde a um problema já conhecido e como contorná-lo. Por exemplo, ao
investigar um incidente, o técnico pode pesquisar pelo erro conhecido na BDEC e aplicar a
## •
## 11
## •
## 30
## 3031
## •
## 32
## 33
## •
## 32
## 34
## 23
## 3530
## 3637
## •
## 1514
## 2
## 3

solução documentada imediatamente, minimizando o impacto sem aguardar a correção
permanente. O sistema deve permitir adicionar um problema à BDEC durante o processo de
gerenciamento de problemas (marcando-o como Erro Conhecido) de forma simples.
Artigos de Solução e Procedimentos Reutilizáveis: Além de erros conhecidos, a base de
conhecimento deve conter artigos gerais: guias de resolução, FAQs, procedimentos e artigos
reutilizáveis que auxiliem na resolução de incidentes e na execução de tarefas de TI. Esses
artigos podem incluir, por exemplo, passo a passo para resolver incidentes comuns (reset de
senha, liberar acesso, etc.), procedimentos de contorno para falhas recorrentes, ou lições
aprendidas de problemas graves. O sistema deve permitir que tais artigos sejam criados e
atualizados pela equipe de suporte ou gestão de conhecimento, possivelmente com um fluxo de
revisão/aprovação para garantir qualidade. Cada artigo deve possuir categorização (por assunto,
serviço, categoria de incidente/problema) e palavras-chave para facilitar a busca.
Mecanismo de Busca e Consulta: Funcionalidade de pesquisa eficiente na base de
conhecimento, permitindo buscas por palavras-chave, filtragem por categoria, tags ou data. Isso
é crítico para que técnicos encontrem rapidamente soluções existentes. A pesquisa deve cobrir
tanto a BDEC quanto os demais artigos (por exemplo, ao digitar um sintoma ou código de erro,
retornar artigos relevantes). Uma base de conhecimento bem mantida torna-se uma das
ferramentas mais poderosas para acelerar tempos de resolução e aliviar a carga de incidentes
. O sistema deve exibir sugestões de artigos correlatos ao registro de um novo incidente (por
ex., ao descrever o incidente, o sistema sugere possíveis soluções conhecidas).
Ligação entre Base de Conhecimento e Incidentes/Problemas: O sistema deve permitir
vincular artigos da base de conhecimento a registros de incidente e problema. Por exemplo,
ao resolver um incidente, o técnico pode associar qual artigo ou erro conhecido foi utilizado na
solução (e idealmente isso poderia ser automaticamente sugerido pelo sistema). Inversamente,
ao concluir a solução de um problema, deve ser possível gerar ou atualizar um artigo na base de
conhecimento com as informações da causa e solução (incluindo marcação de “erro conhecido”).
Essa integração garante reutilização do conhecimento: soluções de contorno e definitivas
documentadas alimentam o catálogo de soluções disponíveis para incidentes futuros.
Além disso, o histórico de quantas vezes um artigo foi consultado ou aplicado pode ser
registrado como indicador (medindo reutilização do conhecimento).
Manutenção e Governança do Conhecimento: Funcionalidades para gestão do ciclo de vida
dos artigos, incluindo revisão periódica (para manter soluções atualizadas), expiração/
arquivamento de soluções obsoletas e controle de versão de artigos. Deve-se também
possibilitar feedback dos usuários técnicos sobre os artigos (ex.: marcar se a solução foi útil) e
métricas de uso. Uma curadoria da base de conhecimento é recomendada, garantindo que as
entradas na BDEC e os artigos estejam corretos e claros. Em suma, a base de conhecimento atua
como memória organizacional de TI, disseminando conhecimento para reutilização por
indivíduos e equipes, possibilitando que conteúdo existente evolua e gere novos
conhecimentos. Implementar uma base de conhecimento robusta com soluções pré-
documentadas ajuda a reduzir tickets repetitivos e acelera as resoluções de incidentes,
além de servir como apoio durante a investigação de problemas.
- Fluxos Principais de Trabalho e Integração Incidente-Problema
Nesta seção descrevemos os principais fluxos operacionais do sistema, enfatizando como a gestão de
incidentes e a gestão de problemas interagem de forma integrada. Os fluxos seguem as práticas
ITIL, garantindo que os processos trabalhem juntos na cadeia de valor do serviço.
## 2
## •
## •
## 38
## •
## 3930
## •
## 40
## 41
## 4243
## 42
## 4

2.1 Fluxo de Gerenciamento de Incidentes
Detecção e Registro: Um incidente pode ser detectado por usuários finais (ex.: abrindo
chamado via portal ou contato com Service Desk) ou por monitorações automáticas que geram
alertas. Ao ser detectado, o incidente é registrado no sistema (abrindo um tíquete de
incidente) com todas as informações relevantes.
Classificação e Prioridade: O analista de suporte classifica o incidente (tipo, serviço afetado,
categoria) e atribui prioridade conforme impacto e urgência. Se for um incidente de alto
impacto (por exemplo, queda geral de um sistema crítico), recebe prioridade máxima e
possivelmente é tratado como Incidente Grave. O sistema pode notificar automaticamente a
coordenação em caso de incidente de alta prioridade ou múltiplos incidentes similares
ocorrendo simultaneamente (detecção de um possível problema).
Resposta Inicial e Diagnóstico: O técnico de nível 1 realiza diagnóstico inicial, tentando
solucionar rapidamente. Ele consulta a Base de Conhecimento em busca de soluções
conhecidas: se encontra um artigo relevante ou um registro na BDEC com solução de contorno
aplicável, implementa-o para restaurar o serviço. Por exemplo, se há um erro conhecido para
“falha de autenticação no sistema X” com um workaround documentado, o técnico aplica esse
workaround e restaura o acesso do usuário. Caso não haja solução conhecida disponível, o
técnico segue com procedimentos de triagem (perguntas ao usuário, testes básicos) e registra
observações.
Escalonamento (se necessário): Se o incidente não puder ser resolvido na linha de frente (Nível
1) – seja pela complexidade ou por ultrapassar um tempo limite (SLA de atendimento) – o
sistema permite escaloná-lo para um grupo de suporte de Nível 2 ou especialistas. O tíquete
mantém todo o histórico já coletado para que o próximo nível continue a investigação. Durante
o escalonamento, notificações são enviadas aos responsáveis. Em caso de incidente grave
(impacto muito alto), há um procedimento de gestão de incidentes major incident, envolvendo
comunicação imediata a gestores e possivelmente acionar o processo de problema
paralelamente.
Investigação e Resolução: A equipe designada (de Nível 2 ou 3) aprofunda a investigação. Se
suspeitar que o incidente tem uma causa desconhecida que possa se repetir, inicia-se um
registro de Problema associado (ver fluxo de problemas abaixo) sem esperar o incidente fechar
– isso ocorre especialmente se vários incidentes semelhantes ocorrem, indicando uma causa
comum. Entretanto, a prioridade na gestão de incidentes é restaurar o serviço o mais rápido possível
, então a investigação profunda de causa raiz pode ser transferida para o gerenciamento de
problemas após a contenção. A equipe então encontra uma solução para resolver o incidente
atual – pode ser uma correção temporária (reiniciar um servidor, por exemplo) ou definitiva
(aplicar um patch conhecido). O tempo decorrido até a resolução é contabilizado pelo sistema
(para métricas de TMRS – Tempo Médio de Recuperação de Serviço). Uma vez aplicada a
ação de recuperação, verifica-se se o serviço voltou ao normal.
Recuperação e Fechamento: Com o serviço restabelecido, o técnico confirma com o usuário
afetado, quando aplicável, que tudo está ok. O incidente então é encerrado no sistema com o
registro da solução adotada e categorização final da causa (se identificada). Por exemplo,
documenta-se que “Incidente X resolvido reiniciando serviço Y; causa provável: saturação de
memória (necessária investigação)”. Se a causa permanecer não confirmada, isso fica indicado e
um problema aberto cuidará de achar a causa. Todos os relacionamentos são mantidos: se esse
incidente estiver vinculado a um Problema no sistema, ele permanece ligado para futura
referência. Após fechamento, o sistema pode atualizar estatísticas (contabilizar um incidente
resolvido, tempo de resolução, etc.).
(Ao longo do fluxo de incidentes, observa-se a importância da integração com  Problemas  e    Base de
Conhecimento: a qualquer momento, técnicos podem consultar erros conhecidos para agilizar a solução,
## 1.
## 44
## 2.
## 11
## 3.
## 30
## 2
## 4.
## 5.
## 42
## 45
## 6.
## 33
## 30
## 5

e se identificam que o incidente é parte de algo maior, escalam para  Gerenciamento de Problema  sem
prejudicar o foco em restaurar o serviço primeiro.)
2.2 Fluxo de Gerenciamento de Problemas
Identificação e Triagem do Problema: Problemas podem ser identificados de duas formas: (a)
Reativamente, após ocorrência de um ou mais incidentes significativos ou recorrentes; o
Service Desk ou as equipes de suporte notam um padrão de falha ou um incidente sem causa
aparente e registram um novo problema relacionado. (b) Proativamente, através de análise
de tendências e monitoramento; por exemplo, revisão mensal de incidentes que revela um
aumento de falhas em determinado sistema, ou alertas de eventos que indicam um possível
futuro incidente grave. Quando uma sugestão de problema é registrada (por um técnico ou
gestor), o Gerente de Problemas avalia sua procedência: verifica informações registradas,
consulta a BDEC para ver se aquele problema ou solução já é conhecido, e checa se já existe um
problema similar em andamento. Se for válido e inédito, o problema é formalizado; se
for duplicado de outro existente, ele é associado ao existente e eventualmente descartado. Ex:
“Múltiplos incidentes de lentidão no banco de dados nas últimas semanas” podem levar à
abertura de um Problema “Investigar causa da lentidão recorrente no BD”.
Registro e Enriquecimento: O problema é então registrado com todos os detalhes disponíveis
(como descrito nas funcionalidades: descrição, serviços afetados, sintomas, incidentes
relacionados, etc.). O sistema pode consolidar automaticamente dados de incidentes ligados:
por exemplo, listar IDs de incidentes vinculados, frequência de ocorrência, desde quando
ocorrem. Nessa fase, o gerente de problemas associa todos os tickets de incidente de mesma
natureza ao problema no sistema, garantindo que haja um vínculo bidirecional (os
incidentes “filhos” apontam para o problema “pai” e vice-versa). Assim, a equipe de problemas
tem uma visão completa do impacto e os atendentes de incidentes sabem que aquele caso está
sendo tratado como problema global.
Classificação e Prioridade: O problema é categorizado e priorizado conforme já descrito.
Problemas recebem uma priorização possivelmente diferente dos incidentes individuais: e.g.,
um problema pode ser de prioridade alta se seus incidentes causam grande impacto cumulativo,
mesmo que incidentes isolados fossem médios. O gerente de problemas define a estratégia de
tratamento (imediato ou pode aguardar, dependendo do risco). Problemas muito graves podem
acionar procedimentos especiais, incluindo informar alta gestão e planejar comunicações (pois
indicam risco sério ao negócio caso não resolvidos).
Investigação e Diagnóstico de Causa Raiz: Esta é a etapa central. O sistema auxilia na gestão
das tarefas investigativas: os técnicos responsáveis podem registrar hipóteses, testes
realizados e resultados. Pode haver integração com o CMDB (Base de Configuração) para
mapear quais componentes de infraestrutura estão envolvidos e se houve mudanças recentes
que possam ter causado o problema. Ferramentas de análise forense ou monitoração
podem ser usadas e anexadas. O processo tende a iterar até descobrir a causa raiz. Durante a
investigação, se for encontrada alguma solução de contorno que mitigue o problema
temporariamente, ela deve ser implementada e registrada imediatamente. Essa solução de
contorno é documentada no problema e também inserida na BDEC como erro conhecido
, para que todos os novos incidentes relativos a esse problema usem o workaround e minimizem
impacto enquanto a correção definitiva não vem. Essa retroalimentação é fundamental: por
exemplo, se durante a investigação do problema de “lentidão no BD” descobre-se que reiniciar
um serviço específico alivia o sintoma, essa ação é informada a todas equipes via BDEC como
workaround sempre que ocorrer a lentidão, até a causa raiz ser removida.
Identificação da Solução e Controle de Erro: Após identificar a causa raiz (por exemplo,
descobriu-se que a lentidão vem de uma configuração incorreta ou bug de software), a equipe
de problemas avalia opções de solução definitiva. Muitas vezes isso envolve propor uma
## 42
## 1.
## 3
## 4
## 4647
## 2.
## 48
## 3.
## 4.
## 49
## 14
## 2
## 2
## 5.
## 6

mudança (correção de código, substituição de hardware, ajuste de configuração) que deve
passar pelo processo de Gerenciamento de Mudanças antes de implementação em produção
. O problema permanece em estado Erro Conhecido enquanto aguarda a mudança: ou
seja, sabemos a causa e possivelmente um contorno, mas a resolução definitiva ainda não está
aplicada. O Controle de Erro é exercido durante esse período – o sistema deve permitir
monitorar erros conhecidos pendentes de solução permanente, incluindo avaliar impacto
contínuo e justificar a prioridade da mudança em termos de custo/benefício. Se por
alguma razão não for possível encontrar solução definitiva viável (ex.: custo muito alto ou
tecnologia legado sem suporte), o problema pode permanecer como erro conhecido
indefinidamente, caso em que o workaround se torna a maneira padrão de lidar com os
incidentes relacionados.
Implementação da Solução Definitiva: Quando a solução permanente está disponível (p. ex.,
após desenvolvimento de patch ou aprovação de mudança), a equipe de problemas coordena
sua implementação. Isso pode significar executar uma Janela de Mudança para aplicar um fix
no ambiente de produção. O sistema de gestão de problemas, idealmente integrado com o de
mudanças, registra a RDM e acompanha a implantação. Durante essa fase, é crucial
comunicar às partes interessadas (Service Desk, usuários-chave) sobre a intervenção e possível
indisponibilidade planejada, embora esse aspecto seja mais de processo do que da ferramenta
em si.
Verificação e Fechamento do Problema: Após aplicar a correção, monitora-se se o problema
foi realmente resolvido – ou seja, se os incidentes pararam de ocorrer e o erro não retorna.
Confirmada a eficácia, procede-se ao fechamento do problema no sistema. Conforme as boas
práticas, no fechamento o sistema deve verificar: (a) Incidentes vinculados – todos os
incidentes relacionados devem ser marcados como resolvidos/fechados, já que a causa raiz foi
eliminada. Se ainda houver incidentes abertos aguardando a resolução do problema, o
sistema pode automatizar a notificação para que os responsáveis fechem-nos informando a
solução permanente aplicada. (b) Documentação na Base de Conhecimento – assegurar que o
conhecimento gerado (causa, solução, procedimentos) foi devidamente registrado. Se o
problema estava na BDEC como erro conhecido, atualizá-lo indicando que agora possui solução
definitiva implementada. (c) Campos obrigatórios de conclusão – o sistema pode exigir
informações como código de causa raiz (para relatórios estatísticos), data da solução, equipe
responsável, etc., antes de permitir concluir. Após isso, o problema é marcado como Encerrado.
Revisão Pós-Resolução: Para problemas de alta gravidade, o processo prevê uma revisão pós-
morte ou análise crítica após o fechamento. O sistema deve permitir registrar essa
revisão, respondendo: todas as atividades foram executadas adequadamente? Houve atrasos ou
dificuldades? O que pode ser melhorado para evitar ou detectar antes esse tipo de problema?
Quais lições aprendidas? Essas informações devem ficar armazenadas (podendo até gerar novos
artigos de conhecimento ou planos de melhoria contínua). Embora essa etapa seja uma prática
de processo, o software pode facilitar fornecendo um template de relatório de revisão para
problemas graves e armazenando-o ligado ao registro do problema.
(O fluxo de problemas acima enfatiza as interações com incidentes: note que incidentes são insumos para
identificar problemas e fornecer dados históricos, e em contrapartida problemas produzem saídas
vitais para incidentes, como soluções de contorno e registros de erros conhecidos. A coordenação entre os
dois processos é fundamental: atividades de gerenciamento de problemas e incidentes devem ser projetadas
para trabalhar juntas, complementando-se – achar a causa de um incidente (função do processo de
problemas) leva à resolução mais completa do incidente –, mas sem conflito – por exemplo, investigar
excessivamente durante um incidente em curso pode atrasar a restauração do serviço. O sistema deve
reforçar essa integração, permitindo linkagem fácil entre incidentes e problemas e visibilidade mútua.)
## 1819
## 5051
## 5253
## 6.
## 1819
## 7.
## 23
## 2354
## 8.
## 2425
## 5556
## 1
## 42
## 7

2.3 Integração entre Incidentes, Problemas e Base de Conhecimento
A integração entre os módulos não é apenas técnica, mas parte do fluxo de trabalho:
Incidente gera Problema: Quando um incidente ou um conjunto de incidentes aponta para
uma causa desconhecida, o agente de suporte pode, diretamente na interface do incidente,
acionar a opção "Registrar Problema" – o sistema então cria um novo registro de problema, já
populado com informações do incidente e linkando-os. Todos os incidentes similares podem ser
associados a esse problema (manual ou automaticamente por regras de correspondência),
formando um grupo. Assim, a equipe de problemas tem acesso aos detalhes de cada incidente e
à frequência, ajudando na investigação.
Problema referencia Incidentes: No registro do problema, deve haver uma lista ou seção
relacionando os incidentes conhecidos atrelados a ele, incluindo status de cada um. Isso permite
que, ao comunicar atualizações (por exemplo, descoberta de um workaround), o responsável
pelo problema possa facilmente notificar os responsáveis por cada incidente. O sistema pode ter
um recurso de broadcast de comentários do problema para todos os incidentes vinculados,
garantindo que a equipe de front-line e até os usuários finais recebam atualização (por exemplo:
“Identificamos a causa e aplicamos uma correção temporária; por favor, testar se o serviço
normalizou”).
Aplicação de Workaround e BDEC: Assim que um erro conhecido é registrado no módulo de
problemas/BDEC, ele deve ficar imediatamente acessível ao módulo de incidentes. Na
prática, isso significa que técnicos de suporte, ao abrir um incidente ou ao buscar soluções,
conseguem achar o registro de erro conhecido e sua solução de contorno. Isso acelera a
resolução dos incidentes relacionados, reduzindo o tempo médio de recuperação (MTTR) e o
impacto aos usuários. O sistema deve, portanto, propagar a informação: por exemplo,
marcando automaticamente todos os incidentes em aberto ligados a um problema como “Erro
Conhecido - workaround disponível”, possivelmente atualizando seu status para Em andamento
(workaround aplicado) se o técnico confirmar a aplicação.
Fechamento em Lote: Quando um problema é resolvido definitivamente, o sistema pode
auxiliar no fechamento coordenado: ele lista todos os incidentes associados que ainda estejam
abertos e oferece a opção de fechar todos, gerando em cada um um registro de solução com
referência ao problema resolvido. Alternativamente, pode notificar os responsáveis por cada
incidente para validar e fechar os tickets. Isso evita que incidentes fiquem esquecidos após a
correção do problema. Conforme o Processo de Fechamento do Problema do IFTO, é
verificado se todos os incidentes relacionados foram encerrados e se a solução foi cadastrada na
BDEC antes de marcar o problema como concluído.
Atualização do Conhecimento: A integração com a base de conhecimento também ocorre no
fechamento do problema: a solução definitiva implementada deve resultar em atualização/
fechamento do registro na BDEC. O sistema poderia, por exemplo, alterar o status do artigo de
“erro conhecido – solução de contorno” para “solução definitiva disponível” ou adicionar os
detalhes da correção permanente ao artigo. Além disso, qualquer lição aprendida ou melhoria
identificada durante a revisão pós-problema pode ser adicionada como artigo na base de
conhecimento geral, ampliando o repositório com conteúdo novo para prevenção de futuros
casos.
Consulta Preventiva: Por fim, a integração permite consulta cruzada para análise proativa: a
equipe de problemas pode consultar estatísticas de incidentes (via módulo de incidentes) para
detectar tendências e pontos fracos, enquanto a equipe de incidentes pode consultar registros
de problemas e conhecimento para orientar atendimentos. Os dois processos alimentam um ao
outro em um ciclo de melhoria contínua – por exemplo, dados de incidentes recorrentes subsidiam
abertura de problemas, e soluções de problemas reduzem a recorrência de incidentes.
## •
## •
## •
## 2
## 31
## •
## 2354
## •
## •
## 4257
## 8

Em resumo, a plataforma deve operar como um sistema  integrado de ITSM, onde incidentes,
problemas e conhecimento não são silos, mas componentes interligados. Uma implementação bem-
sucedida unifica esses processos num só lugar, evitando retrabalho e acelera a restauração de serviços
. Isso garantirá que as equipes de suporte tenham visibilidade completa: ao olhar um incidente
crítico, saberão se existe um problema raiz em tratamento; ao investigar um problema, saberão
quantos incidentes ele causa; e sempre terão à disposição o  histórico de soluções  na base de
conhecimento para guiá-los.
- Requisitos Funcionais e Não Funcionais
Nesta seção enumeramos os principais requisitos funcionais (o que o sistema deve fazer) e não
funcionais (qualidades e restrições do sistema) para o software de gestão de problemas/incidentes/KB.
## 3.1 Requisitos Funcionais
Registro e Controle de Incidentes: O sistema deve possibilitar o registro de incidentes com
campos obrigatórios (categoria, descrição, solicitante, serviço afetado, prioridade, etc.) e
acompanhar seu status do início ao fim. Deve suportar fluxos de trabalho de incidente, incluindo
atribuição a agentes, escalonamento de nível, suspensão/pendência (quando aguardando
terceiro) e fechamento com documentação final. Todo incidente deve ter um identificador único
e audit trail das atualizações.
Registro e Controle de Problemas: Deve ser possível criar registros de problema
independentemente ou a partir de um ou mais incidentes. O problema terá seus próprios
campos (descrição detalhada, sintomas, impacto, causa raiz, solução de contorno, solução
definitiva, etc.) e um workflow similar: estados como Novo, Em Análise, Erro Conhecido,
Aguardando Mudança, Resolvido, Fechado. Permitir associar múltiplos incidentes relacionados a
um problema e vice-versa. Incluir funcionalidades para gerenciar tarefas dentro do problema
(por exemplo, passos da investigação) pode ser desejável.
Base de Conhecimento Integrada: O software deve incluir uma base de conhecimento interna
onde artigos e erros conhecidos são armazenados. Deve haver funções para criar, editar, revisar
e publicar artigos de conhecimento. Os artigos da BDEC (erros conhecidos) devem poder ser
criados diretamente a partir de problemas ou manualmente. A base de conhecimento deve ser
pesquisável e integrada aos módulos: técnicos devem conseguir consultar soluções durante o
registro ou tratamento de incidentes, e gerentes de problema devem verificar se já há
conhecimento prévio sobre um novo problema.
Linkagem e Referenciamento: Requisito fundamental é a capacidade de vincular registros:
vincular um incidente a um problema (e ver essa relação em ambas as entidades), e associar
artigos de conhecimento a incidentes ou problemas. Por exemplo, em um ticket de incidente
deve haver um campo “Relacionado a Problema nº X” clicável para navegar, e no registro do
problema uma lista de “Incidentes vinculados”. Semelhantemente, em um incidente resolvido,
poder referenciar “Artigo de KB utilizado”. Essa rastreabilidade permite navegabilidade e análise
de impactos.
Notificações e Alertas: O sistema deve enviar notificações automáticas em eventos
importantes, ajustáveis conforme papéis. Exemplos: notificar um técnico quando um incidente
lhe for atribuído; notificar o gerente de problemas quando um novo problema for aberto; avisar
os responsáveis quando um incidente está violando SLA ou ficou muito tempo sem atualização;
avisar os técnicos de incidentes vinculados quando um problema tem uma solução de contorno
disponível ou foi resolvido, etc. As notificações podem ser por e-mail e/ou internas (painel,
push). Idealmente, permitir configurar regras de alerta customizadas (ex.: um alerta diário de
incidentes críticos abertos).
## 58
## •
## •
## •
## 30
## •
## •
## 9

Catálogo de Categorias e Serviços: Possuir um cadastro administrável de categorias de
incidente/problema, categorias de artigo de conhecimento, e lista de serviços/ativos atendidos.
Isso garante consistência na classificação. Ex: categorias como Software, Hardware, Rede, etc., e
subcategorias específicas. Também integrar com um Catálogo de Serviços (se existir) para
referenciar qual serviço ou aplicação está impactado pelo incidente/problema. Essa
estrutura possibilita relatórios por categoria/serviço, e ajuda na atribuição automática (ex.:
problemas de Rede vão para equipe X).
Pesquisa e Relatórios: Funções de busca filtrada de tickets (incidentes e problemas) por
diversos critérios (status, prioridade, categoria, palavra-chave no texto, datas, responsável, etc.).
Módulo de relatórios que permita extrair informações e indicadores, como quantidade de
incidentes por mês, por serviço, tempo médio de resolução por prioridade, quantidade de
problemas abertos/fechados, entre outros. O sistema deve oferecer alguns relatórios padrão e
possibilitar criação de painéis personalizados com KPIs em tempo real. Por exemplo, um
painel de operador mostrando seus chamados abertos e próximos do SLA, e um painel de gestor
com visão agregada.
Controle de SLA: Capacidade de configurar Acordos de Nível de Serviço (SLA) para diferentes
tipos de incidente (ex.: prioridade Alta – resolver em 4h, Média em 24h, etc.) e acompanhar seu
cumprimento. O sistema deve calcular tempos (abertura até resolução) e destacar incidentes
que estão próximos de violar o SLA ou que já estouraram o prazo. Indicadores de SLA podem
alimentar os dashboards. Embora atualmente não haja integrações obrigatórias, essa
funcionalidade prepara o sistema para trabalhar com monitoramento de SLAs e possivelmente
enviar métricas a ferramentas externas, se necessário.
Controle de Acesso e Perfis de Usuário: Implementar perfis/papéis de usuário com
permissões adequadas. Por exemplo: Técnico de Suporte pode criar/atualizar incidentes,
consultar problemas e KB; Gestor de Problemas pode criar/editar problemas, associar incidentes
e atualizar status; Gerente pode acessar dashboards gerenciais e configurar categorias;
Contribuidor de Conhecimento pode criar artigos e submeter para aprovação; etc. Deve haver
autenticação de usuários (com preparação para suportar autenticação unificada no futuro, como
LDAP/AD ou SSO) e autorização baseada em função, para que informações sensíveis fiquem
restritas (por ex., incidentes de determinado departamento visíveis só para times específicos).
Usabilidade e Registro Simplificado: O sistema deve facilitar o registro rápido de tickets, com
interface amigável e campos relevantes para cada tipo. Por exemplo, ao abrir um incidente,
sugerir campos dinamicamente conforme categoria (incident templates). Fornecer portal de
autoatendimento não é prioritário se focado apenas em usuários técnicos, mas eventualmente
pode-se considerar uma interface simplificada para que usuários finais registrem solicitações e
consultem a base de conhecimento por conta própria. Mesmo internamente, a facilidade de
uso é crucial: telas claras, possibilidade de atualização em massa (ex.: fechar vários incidentes
vinculados de uma vez), e recursos de colaboração (comentar, mencionar colegas em um ticket,
anexar arquivos) aumentam a eficiência.
Registro de Histórico e Auditoria: Todas as ações relevantes devem ser registradas (quem
mudou status, quem adicionou comentário, quando). Um log de auditoria é necessário
especialmente para processos ITIL, garantindo conformidade e facilitando análise de
retrospectiva. Por exemplo, em um incidente: “08:30 Usuario X abriu incidente, 08:45 Grupo Y
atribuído, 09:10 priorizado como Alto, 09:30 escalonado para N2, 10:00 resolvido por Usuario Z
com solução...”. Isso também ajuda no pós-análise de problemas e incidentes graves, para
entender os tempos e atrasos.
Preparado para Integrações Futuras: Embora não haja integrações imediatas obrigatórias, o
sistema deve ser concebido para interoperar facilmente. Isso implica disponibilizar APIs
(RESTful) para operações principais (criar/consultar/atualizar incidentes, problemas, artigos),
facilitando integrações com outros sistemas de TI no futuro (como sistemas de chamados
legados, ferramentas de monitoramento que abram incidentes automaticamente, sistemas de
## •
## 58
## •
## 59
## •
## •
## •
## 60
## •
## •
## 10

autenticação centralizada, etc.). Também ser capaz de exportar/importar dados em formatos
padrão (CSV, JSON) para migração ou reporting externo. Esse requisito visa proteger o
investimento, garantindo que o software possa se conectar a um ecossistema ITSM maior
conforme necessário.
Módulos Adicionais Futuramente: O design funcional deve ser modular o suficiente para
incorporar novos processos ITIL futuramente, como Gerenciamento de Mudanças,
Configuração (CMDB), Catálogo de Serviços, etc., numa mesma plataforma. Por exemplo, se
em próximo passo desejar incluir gestão de mudanças, o sistema já teria a entidade “RDM”
pronta para se relacionar com problemas. Essa visão modular evita retrabalho futuro e favorece
uma plataforma única de gestão de serviços.
## 3.2 Requisitos Não Funcionais
Escalabilidade e Desempenho: O sistema deve suportar um volume considerável de registros e
usuários simultâneos sem degradação significativa de performance. Operações comuns (abrir
chamado, atualizar status, buscar conhecimento) devem ter tempos de resposta curtos (ex.: <2
segundos). A arquitetura deve permitir escalabilidade horizontal ou vertical conforme o
crescimento do uso – por exemplo, possibilidade de distribuir carga entre múltiplos servidores
de aplicação.
Disponibilidade e Confiabilidade: Considerando que o software será utilizado por equipes de
suporte para gerir incidentes de TI, ele próprio deve ter alta disponibilidade (idealmente 24x7 ou
pelo menos dentro do horário de suporte crítico). Qualquer indisponibilidade do sistema de
gestão impacta a capacidade de resolver incidentes. Portanto, requisitos como redundância
(deploy em servidores redundantes, backups frequentes do banco de dados) e plano de
recuperação de desastres são importantes. Além disso, o sistema deve ser confiável, ou seja,
não apresentar falhas que causem perda de dados de chamados ou corrupção de informações.
Segurança: Implementar boas práticas de segurança da informação. Controle de acesso robusto
(já citado em funcional), proteção contra acessos não autorizados – possivelmente integração
com autenticação corporativa (SSO) no futuro. Criptografia de tráfego (HTTPS obrigatório) e
criptografia de dados sensíveis em repouso (ex.: senhas hash, campos confidenciais cifrados se
necessário). Preocupação com confidencialidade: incidentes podem conter informações
sensíveis de negócio, então somente pessoas autorizadas devem vê-los (ex.: incidente de RH
visível só para TI e RH). O sistema deve manter um registro de auditoria de acessos e edições
para deter abuso. Também deve ser desenvolvido seguindo padrões de segurança (prevenção
de SQL injection, XSS, etc.).
Usabilidade e Acessibilidade: A interface deve ser intuitiva e consistente. Usuários técnicos
devem conseguir navegar entre Incidentes, Problemas e KB facilmente. Deve haver indicadores
visuais claros de prioridade (ex.: cor ou ícone para incidentes críticos), SLA (um relógio regressivo
talvez). Ferramentas como filtros, painéis personalizáveis e campos auto-sugestivos (auto-
complete de categorias, por exemplo) melhoram a usabilidade. Além disso, considerar
acessibilidade para usuários com necessidades especiais (compatibilidade com leitores de tela,
bom contraste, etc.) é recomendável. Um sistema fácil de usar reduz erros de operação e
treinamento necessário.
Compatibilidade e Portabilidade: O software deve ser acessível via navegadores web
modernos sem requerer plugins proprietários. Suporte responsivo para diferentes tamanhos de
tela (por exemplo, permitir consultas rápidas via tablets ou celulares pelos técnicos em plantão)
é um diferencial. Se for uma aplicação web, garantir compatibilidade com Chrome, Firefox, Edge,
etc. Caso haja client desktop ou mobile no futuro, fornecer APIs abertas ajuda nisso. Além disso,
se for implantado on-premises, deve rodar em ambientes padrão (servidor com sistema
operacional comum, banco de dados suportado). Se for SaaS, deve suportar múltiplos clientes
isolados (multi-tenancy) possivelmente.
## •
## 58
## •
## •
## •
## •
## •
## 11

Modularidade e Manutenibilidade: O design interno deve ser modular, facilitando manutenção
e evolução. Alterações em um módulo (por exemplo, atualização no fluxo de problemas) não
devem impactar indevidamente outros módulos (incidentes, conhecimento). Código limpo,
documentado e arquitetura em camadas (separando frontend, backend, lógica de negócio,
acesso a dados) são importantes. A existência de APIs internas bem definidas entre módulos
(mesmo que monolítico, com interfaces claras) tornará mais fácil integrar novas funcionalidades
ou trocar componentes (por ex., substituir o mecanismo de busca da base de conhecimento sem
refatorar todo o sistema). Em resumo, a arquitetura deve facilitar atualizações e correções de
bugs, com baixo acoplamento e alta coesão.
Auditabilidade e Conformidade: O sistema deve permitir gerar evidências para auditorias de
processos, se necessário. Por exemplo, exportar um relatório de todas as mudanças de status de
um incidente ou problema, para comprovar tempos de atendimento (útil em auditorias de SLA
ou de qualidade). Seguir as melhores práticas ITIL também é uma forma de conformidade (ITIL
não é uma norma, mas algumas organizações buscam ISO 20000, e um software alinhado ao
ITIL ajuda a cumprir requisitos). Logo, manter registros históricos e fornecer meios de monitorar
a conformidade do processo (se todos os campos obrigatórios foram preenchidos, se prazos de
SLA estão sendo cumpridos, etc.) é um requisito não funcional relevante para governança.
Performance de Busca e Armazenamento: Considerando a base de conhecimento e volume de
chamados, a aplicação deve ter mecanismos eficientes de busca textual e filtragem. Isso pode
envolver indexação de conteúdo (talvez uso de um mecanismo de search engine dedicado para
pesquisar nos textos de descrição e artigos). Do ponto de vista de armazenamento, o banco de
dados deve suportar milhares de registros de incidentes/problemas e consultas complexas.
Planejar estratégias de arquivo de tickets antigos (ex.: fechar e arquivar incidentes com mais de
X anos para não degradar consultas diárias) também é válido dependendo do crescimento.
Internacionalização e Localização: Como é direcionado ao contexto brasileiro, a interface
estará em Português (Brasil). Ainda assim, seria positivo prever internacionalização (suporte a
outros idiomas) caso no futuro equipes de outros locais venham a usar, ou para conformidade
com terminologias (por ex., usar termos em português alinhados com ITIL traduzido).
Integração Facilitada com Futuras Ferramentas: Reforçando o mencionado nos funcionais,
um requisito não funcional é ter uma arquitetura orientada a serviços (SOA) ou API-first, de
modo que integrar com ferramentas de terceiros seja tecnicamente simples. Por exemplo,
integrar com uma plataforma de monitoramento que automaticamente crie incidentes via API
quando um alarme dispara, ou integrar com sistemas de autenticação (OAuth2, SAML para SSO),
ou ainda com ferramentas de comunicação (como MS Teams, Slack para notificar canais de
incidentes críticos). Essa predisposição técnica (usar protocolos padrão, ter webhooks e API bem
documentada) aumenta o valor do sistema a longo prazo.
## 4. Arquitetura Técnica Recomendada
Para suportar os requisitos acima, recomenda-se uma arquitetura modular e escalável. Uma possível
abordagem é dividir o sistema em camadas e serviços, conforme descrito a seguir:
Arquitetura em Camadas: Separe claramente as camadas de apresentação, lógica de negócio e
dados. A camada de apresentação seria a interface web (e possivelmente móvel), responsável
por exibir os painéis, formulários de chamados, etc. A camada de negócio implementa as regras
de ITIL (fluxos de estado de incidente/problema, validações de SLA, envio de notificações). A
camada de dados consiste no banco de dados e possivelmente mecanismos de busca e cache.
Essa separação facilita manutenção e futuras expansões.
Backend Modular ou Microsserviços: Internamente, pode-se optar por uma arquitetura de
microsserviços ou módulos desacoplados que refletiriam as funções principais: um serviço para
Incidentes, um para Problemas, um para Conhecimento, etc. Cada serviço teria sua lógica
## •
## •
## •
## •
## •
## •
## •
## 12

encapsulada, expondo APIs internas. Por exemplo, o serviço de Knowledge Base cuidaria de
salvar e buscar artigos, enquanto o de Incidentes cuidaria de operações de incidentes. A
vantagem é poder escalar e atualizar módulos independentemente e, se necessário, implantar
somente parte do sistema (embora integradas, as APIs permitiriam até usar um módulo sem
outro, se quisesse integrá-lo a outra solução). Contudo, uma abordagem mais simples
inicialmente é um sistema monolítico bem organizado em módulos de código (modular
monolith), evoluindo para microsserviços conforme a necessidade. O importante é adotar
interfaces claras entre módulos, mesmo que todos rodem juntos.
APIs e Integração: Expor APIs RESTful para as principais entidades e operações do sistema.
Isso envolve definir endpoints como /api/incidents, /api/problems, /api/knowledge
com métodos GET/POST/PUT etc. protegidos por autenticação. Tais APIs permitirão integrações
externas (futuro aplicativo móvel, integração com outras ferramentas ITSM, chatbot, etc.).
Adicionalmente, o sistema pode oferecer webhooks para eventos (ex.: enviar um POST a uma
URL configurada quando um incidente crítico é aberto, para integrar com um sistema de
alertas). A arquitetura deve suportar facilmente a adição de novas integrações – por exemplo,
adicionar um conector para um sistema de autenticação unificada (OAuth2/OpenID Connect) ou
para importar usuários de um AD.
Banco de Dados: Utilizar um banco de dados relacional robusto (como MySQL, PostgreSQL ou
SQL Server) para armazenar os registros de incidentes, problemas, artigos e configurações.
Esses dados têm estruturas bem definidas e relacionamentos (ex.: muitos incidentes vinculados
a um problema, artigos referenciando problemas, etc.), o que se alinha a um modelo relacional.
Tabelas principais poderiam incluir: Incidents, Problems, KnowledgeArticles,
IncidentProblemLinks (tabela associativa), etc. O BD deve ser projetado com integridade
referencial (ex.: não permitir deletar um problema que tenha incidentes vinculados sem
tratamento) e indices adequados para performance (indexar campos usados em busca, como
status, categoria, data). Para a parte de busca textual nos campos de descrição e conteúdo de
artigos, pode-se usar funcionalidades de full-text search do próprio SGBD ou acoplar um engine
de busca dedicado (como Elasticsearch) sincronizado com o banco. A escolha depende do
volume e da necessidade de busca avançada.
Camada de Busca/Indexação: Se a base de conhecimento for grande ou precisar de busca
avançada (relevância, fuzzy search), a arquitetura pode incluir um componente de search
indexing. Por exemplo, cada vez que um artigo de conhecimento é criado ou atualizado, indexá-
lo em um servidor de busca. Isso melhora a rapidez e inteligência das consultas de
conhecimento sem sobrecarregar o banco relacional. Esse componente pode ser escalado
separadamente e otimizado para consultas textuais.
Notificações e Comunicação: Para implementar notificações, é útil ter um mecanismo de fila
de mensagens ou serviço de job scheduler. Por exemplo, ao ocorrer um evento (incidente
escalado), o sistema publica uma mensagem numa fila que um serviço de notificações consome
e envia e-mails. Isso desacopla o envio de notificações do fluxo principal (evitando travar o
usuário ao salvar um incidente esperando e-mail enviar). Tecnologias como RabbitMQ, AWS SQS
ou mesmo agendadores internos podem ser utilizados. Alternativamente, pode-se usar serviços
push/websocket para notificações em tempo real na interface web (por ex., um painel de gestor
que atualiza assim que um incidente crítico chega). A arquitetura deve contemplar isso se for
requisito – podendo inicialmente ser simples (só e-mail) mas extensível para push real-time.
Cliente Web e UX: Adotar tecnologias web modernas (por ex., framework JavaScript como React,
Angular ou Vue) para construir uma interface rica e responsiva. Isso permite criar uma
experiência de usuário dinâmica – ex.: arrastar e soltar para reordenar painéis, atualização
automática de filas de incidentes, etc. A aplicação web consumiria as APIs mencionadas acima.
Importante garantir que o front-end seja modularizado por funcionalidade (tal como o backend)
– por exemplo, ter componentes/menus para Incidentes, Problemas, Knowledge, e carregar
## •
## •
## •
## •
## •
## 13

apenas o necessário. Para gerenciamento de estados e offline (se for necessário), considerar um
design que permita continuidade (mas offline talvez não seja crucial).
Autenticação/Autorização: A arquitetura deve incorporar um módulo de autenticação,
preferencialmente baseado em padrões (JWT tokens para APIs, por exemplo). Isso facilita
integrar com SSO futuro. Inicialmente pode usar login/senha internos, mas projetar de forma
que se possa trocar para um Identity Provider externo sem grandes mudanças. A autorização
por perfis pode ser implementada no backend (verificando permissões em cada endpoint) e
reforçada no frontend (escondendo botões que usuário não deve usar).
Deploy e Infraestrutura: O sistema deve ser implementável tanto on-premises quanto em
nuvem, conforme necessidade da instituição. Recomenda-se uso de contêineres (Docker) para
facilitar deploy consistente em diferentes ambientes (desenvolvimento, homologação,
produção). A arquitetura pode ser preparada para orquestração em Kubernetes ou outra
plataforma caso escalabilidade seja necessária. Se microsserviços forem usados, orquestração e
descoberta de serviços entram em jogo, mas se monolítico modular, um contêiner único pode
bastar. De qualquer forma, separar configurações do código (por ex., strings de conexão,
credenciais de e-mail) para facilitar manutenção.
Integração com E-mail e Outros Serviços: Módulos para integração com servidores SMTP (para
envio de e-mails de notificação) e possivelmente APIs de chat (Teams/Slack) ou SMS se alertas
críticos precisarem. A arquitetura deve permitir plugin dessas integrações sem modificar a lógica
central – por exemplo, via um adapter ou serviço de notificação configurável.
Monitoramento e Logs: Incluir no design pontos de monitoramento – por exemplo, expor
métricas de aplicação (número de tickets abertos, throughput de requisições) via endpoints de
health, para integrar com ferramentas de monitoração. Também definir estratégia de logs
centralizados para depuração (cada ação importante logada, erros de aplicação registrados com
detalhes para diagnóstico). Isso garante que a operação e a evolução do sistema sejam bem
suportadas.
Segurança na Arquitetura: Levar em conta segurança desde o início: usar frameworks seguros,
componentes atualizados, e segmentar a arquitetura para minimizar danos caso um
componente seja comprometido. Por exemplo, se usar microsserviços, garantir uso de
certificados e autenticação mútua nas comunicações entre serviços sensíveis. No banco de
dados, aplicar princípio de mínimo privilégio (a aplicação usa um usuário DB com apenas as
permissões necessárias). Realizar backups regulares do BD e ter um plano de restore. Todas
essas considerações arquiteturais garantem que o sistema atenda requisitos críticos de
confiabilidade para uma ferramenta de suporte de TI.
Em suma, a arquitetura recomendada é a de uma plataforma ITSM modular, unificando processos de
incidentes, problemas e conhecimento, com APIs abertas e componentes bem definidos (UI, lógica,
dados). Isto elimina silos operacionais e facilita colaboração entre equipes, assegurando consistência
na  entrega  de  serviços.  Além  disso,  recursos  como  automação de fluxos  (ex.:  atribuição
automática, notificações) e integração de conhecimento e ativos (ex.: ligação com CMDB no futuro)
devem estar na base da arquitetura, pois são fatores de eficiência e qualidade. Com essa base técnica, o
sistema poderá crescer para abarcar outros processos (mudança, ativos, catálogo) e se integrar ao
ecossistema de TI da organização de forma fluida.
- Interface do Usuário para Equipe Técnica e Gestão
O sistema deverá oferecer interfaces diferenciadas (ou pelo menos, recursos diferentes) para usuários
técnicos de suporte  e    usuários de gestão, adequando-se às necessidades de cada perfil, mas
mantendo uma experiência unificada. A seguir descrevemos as expectativas de interface:
## •
## •
## •
## •
## •
## 58
## 14

5.1 Interface para Usuários Técnicos (Operacional)
Este é o ambiente usado no dia a dia pelos analistas de suporte (Service Desk, técnicos de N1/N2,
especialistas) e possivelmente pelos desenvolvedores que atuam na resolução de problemas. As
características incluem:
Visão de Filas de Trabalho: Uma dashboard inicial mostrando ao técnico os itens que requerem
sua atenção. Por exemplo, uma lista de Meus Incidentes Abertos, Incidentes da minha equipe,
Problemas em investigação atribuídos a mim e possivelmente um widget de Notificações (ex.: “5
incidentes próximos do SLA”, “novo comentário em Problema X”). Isso ajuda o técnico a priorizar
suas atividades assim que entra no sistema.
Lista e Detalhe de Incidentes: Uma interface para listar incidentes com filtros (por status,
prioridade, fila, etc.) e ordenação. Cada incidente listado mostra campos essenciais (ID, resumo,
solicitante, prioridade, status, data). Ao clicar, abre-se o detalhe do incidente, exibindo todas as
informações em abas ou seções: detalhes básicos, conversas/comentários, histórico de status,
itens vinculados (problema relacionado, artigos sugeridos), etc. Aqui o técnico pode atualizar o
ticket: alterar status, atribuir a outro grupo, adicionar comentário (com opção de marcar privado
ou público para usuário), e registrar resolução. Se o incidente estiver vinculado a um problema,
isso deve ficar destacado (ex.: um banner “Este incidente faz parte do Problema #123 – link”).
Também deve haver facilidade para consultar e anexar artigo da base de conhecimento. Por
exemplo, um botão “Pesquisar solução” que permita digitar palavras-chave e retorne artigos e
erros conhecidos relacionados; ao selecionar um artigo, ele pode ser anexado ao incidente e seu
conteúdo visível, auxiliando o técnico.
Registro/Criação Rápida: Uma tela (ou formulário modal) de novo incidente para uso do
Service Desk ao atender uma chamada. Focada em rapidez, com campos essenciais no topo
(usuário, resumo, serviço) e demais campos agrupados. Possibilidade de procurar usuário em
diretório, de categorizar via menus suspensos pré-definidos. Talvez suporte a plantillas
(templates) para incidentes comuns, preenchendo automaticamente descrição padrão.
Similarmente, caso um técnico precise abrir um Problema, a tela de novo problema deve coletar
informações relevantes, mas ela pode ser pré-preenchida se originada de incidentes
selecionados.
Interface de Problemas: Para usuários técnicos envolvidos em gerenciamento de problemas
(talvez um grupo menor, como especialistas ou gestores de problema), deve haver uma visão de
lista de problemas em curso. Parecido com a de incidentes, com filtros (por status, prioridade
do problema, serviço afetado). Selecionar um problema mostra o detalhe do problema com
seções: descrição e informações básicas, lista de incidentes relacionados (com links), campo de
causa raiz (preenchido quando descoberto), workaround (se houver), e histórico de ações/
comentários. O sistema deve permitir que técnicos adicionem notas de investigação (por
exemplo, um log das atividades de troubleshooting realizadas) e anexos. Também deve permitir
atualizar status (ex.: mover para “Erro Conhecido” ou “Aguardando mudança”) e registrar a
solução definitiva quando aplicada. Se o problema requer abertura de uma mudança, talvez um
botão “Criar RDM” para integrar com mudança (se existir) ou ao menos um campo para
referenciar o ID da mudança externa.
Base de Conhecimento para Técnicos: Provavelmente acessada via um menu “Conhecimento”
ou via a busca integrada nas telas de incidente/problema. Uma interface de pesquisa global (ex.:
uma barra no topo “Pesquisar na base de conhecimento...”) que ao digitar mostre sugestões de
artigos. Também uma tela de lista de artigos navegável por categoria, útil para browsing (por
ex.: categoria Rede – mostra todos artigos sobre rede). Técnicos devem conseguir marcar artigos
como favoritos ou úteis, e possivelmente comentar (embora o comentário público talvez seja
restrito a uma função de Knowledge Manager para moderar). Um técnico também poderia
propor um novo artigo, por exemplo ao fechar um incidente que não tinha conhecimento prévio,
## •
## •
## •
## •
## •
## 15

poderia ter um checkbox “Cadastrar solução na base de conhecimento” que ao fechar abre um
formulário de novo artigo pré-preenchido com detalhes do incidente. Isso torna a captura de
conhecimento mais fluida.
Usabilidade focada em produtividade: Para técnicos, é importante que a interface ofereça
atalhos e minimização de clique. Exemplos: possibilitar editar certos campos inline sem abrir
tela separada; arrastar e soltar para reordenar colunas ou priorizar; usar ícones claros (ex.: um
relâmpago para incidentes graves, um símbolo de livro aberto indicando que há artigos
sugeridos). A interface deve atualizar estados em tempo real se possível (ex.: um incidente
desaparece da fila quando outro agente o assume). Ferramentas de busca rápidas (um ctrl+K
para buscar tickets pelo ID ou título, por exemplo) agilizam o trabalho.
Multi-dispositivo: Enquanto a maior parte do uso técnico será em desktops, pode haver
situações de suporte em campo ou plantão. A interface web deve ser responsiva o suficiente
para pelo menos consultar e comentar em incidentes via smartphone. Se no futuro um app
móvel for criado, as APIs preparadas suportarão isso; mas desde já um design responsivo ajuda.
5.2 Interface para Usuários de Gestão (Gerencial)
Os gestores – coordenadores de suporte, gestores de TI, product owners – usarão o sistema para visão
macro, tomada de decisão e configuração. As necessidades deles são cobertas por:
Dashboards de Indicadores: Ao fazer login, um gestor deve ter acesso a painéis consolidados
mostrando os principais indicadores de performance e status. Por exemplo: Número de
Incidentes Abertos por Prioridade, Tempo Médio de Resolução (TMRS) atual, % de SLAs
atendidos, Incidentes Recorrentes identificados no mês, Problemas Abertos vs Fechados no
ano, etc. Gráficos de pizza, barras ou linha facilitam visualizar tendências (ex.: queda ou
aumento de volume de incidentes). Esses painéis devem ser customizáveis – talvez o gestor
possa escolher quais widgets ver. O importante é oferecer KPI em tempo real e histórico para
apoiar decisões. Por exemplo, se o dashboard mostra um crescente número de incidentes
em um serviço crítico, o gestor já considera acionar um gerenciamento de problemas proativo.
Relatórios Detalhados: Além de visualizações, gestores precisam extrair relatórios com dados
crus ou detalhados. O sistema deve fornecer relatórios como: lista de todos incidentes do mês
com tempo de resolução e responsável (para avaliar performance individual ou cumprimento de
SLA), relatório de problemas graves ocorridos no ano e suas causas (para reuniões de post-
mortem), artigos de conhecimento mais acessados, etc. Possibilitar exportar esses relatórios
(CSV/PDF) para uso em apresentações ou auditorias. Talvez um agendador de relatórios seja
útil (ex.: enviar automaticamente todo mês um relatório para o e-mail do gestor).
Visão de Controle de Chamados: Gestores podem precisar intervir em chamados e
supervisionar o andamento. Uma visão global de incidentes (similar à dos técnicos, mas
abrangendo todos os grupos) com filtros por equipe ou localidade permite ver gargalos. Por
exemplo, um gerente pode filtrar “Incidentes críticos abertos” para assegurar que todos estão
sendo tratados. Ele também deve conseguir reatribuir incidentes entre filas se necessário, ou
aprovar rejeição de chamados se for o caso. Entretanto, a interface gerencial não deve ser
confusa com detalhes de operação – a ênfase é em monitoramento e controle, não em
execução de cada passo.
Gestão de Problemas e Mudanças: O gestor (ou product owner) pode estar interessado nos
problemas em andamento, pois estes refletem melhorias estruturais ou defeitos em produtos.
Uma tela de portfólio de problemas poderia listar todos os problemas abertos, com
informações como impacto previsto, status (em análise, aguardando fix etc.), e responsável. Isso
fornece ao gestor uma noção das dívidas técnicas ou riscos que a TI está endereçando. Poderia
até priorizar junto com equipes: exibir prioridade do problema e permitir reordenar (se for
## •
## •
## •
## 6162
## 59
## •
## •
## •
## 16

responsável por determinar quais causas-raiz resolver primeiro). Se integrado com mudança, ver
o status das mudanças relacionadas (planejada, em andamento, concluída).
Configurações e Admin: Gestores de TI ou administradores do sistema precisarão de uma
interface para configurar parâmetros: gerenciamento de usuários e permissões, listas de
categorias e serviços, regras de SLA, templates de notificações, etc. Essa parte da interface deve
ser restrita a administradores. Pode ser algo como um menu de Configurações com sub-telas
para cada entidade configurável. Por exemplo, em “Categorias” poder adicionar/editar
categorias de incidente e problema; em “Usuários” atribuir papéis; em “SLA” definir tempos por
prioridade. Uma configuração importante é a malha de prioridade (impacto vs urgência) –
seria ótimo se o sistema permitisse editar a matriz ou os critérios que definem prioridade
automaticamente.
Acompanhamento de SLA e Qualidade: A interface gerencial deve facilitar identificar
incidentes fora do padrão. Pode haver uma tela específica de monitor de SLA, destacando
incidentes que violaram ou vão violar SLA em breve, para que gestores atuem (realocar recursos,
por exemplo). Também, métricas como satisfação do usuário final (se for coletada via pesquisa
após fechamento de chamados) podem ser exibidas, para avaliar qualidade do suporte.
Supporte à Decisão e Melhoria Contínua: Idealmente, as telas gerenciais não só apresentam
números mas ajudam a interpretá-los. Por exemplo, um dashboard poderia mostrar “Top 5
categorias de incidentes” e ao lado “Tem um Problema aberto para cada uma dessas
categorias?” sinalizando se sim ou não – encorajando comportamento proativo. Ou “Incidentes
Recorrentes” identificados automaticamente (um módulo analítico detectando vários incidentes
com descrição similar) e sugerindo “Candidate a Problema”. Essas inteligências podem ser
incrementais, mas valem menção. Em suma, a interface de gestão deve transcender listagens e
permitir insights – seja via comparações, tendências ao longo do tempo, ou cruzando dados de
incidentes x problemas x conhecimento para evidenciar gaps.
Resumindo, a UI de gestão foca em visão ampla, análise e configuração, enquanto a UI operacional
foca em eficiência na resolução de casos individuais. Ambas convivem na mesma aplicação, mas
compondo diferentes perspectivas. Essa separação de visões também reforça a claridade: cada usuário
vê o que é mais relevante para suas tarefas, tornando o sistema mais limpo e útil.
(Observação: tanto usuários técnicos quanto gestores se beneficiarão da integração com a base de
conhecimento na interface. Por exemplo, gestores podem ter um relatório de “Conhecimento reutilizado”
mostrando quantos incidentes foram resolvidos com ajuda de artigos – um indicador de eficácia da base de
conhecimento. Já técnicos têm a busca no contexto do atendimento. Assim, a interface deve tornar a consulta
ao conhecimento algo natural durante as atividades, ao invés de silo separado.)
- Indicadores e Painéis de Monitoramento Relevantes
Por fim, definimos os principais  indicadores de desempenho (KPIs)  e elementos de  painéis de
controle que o software deve fornecer para monitorar a eficácia do suporte e orientar melhorias,
conforme práticas de ITIL e metas organizacionais. Esses indicadores se alinham aos objetivos do
processo de gestão de incidentes e problemas (restaurar serviços rápido, eliminar causas raiz, reduzir
recorrências, etc.).
Alguns indicadores e métricas-chave incluem:
TMRS (Tempo Médio de Recuperação de Serviço): Também conhecido como MTTR (Mean Time
to Restore). Mede o tempo médio desde o registro de um incidente até sua resolução e
restabelecimento do serviço. É calculado geralmente em horas. Pode ser segmentado por
prioridade (MTTR para incidentes críticos, altos, etc.). Esse indicador mostra eficiência do
## •
## •
## •
## 6364
## •
## 45
## 17

processo de incidente: quanto menor, melhor. O painel deve mostrar o TMRS atual e sua meta, e
acompanhar tendência mensal. Uma redução contínua do TMRS indica melhoria na capacidade
de resolver incidentes rapidamente, possivelmente graças a knowledge base e problem
management atuante.
Número de Incidentes Recorrentes: Este indicador identifica incidentes repetitivos que
ocorrem múltiplas vezes pelo mesmo motivo. Pode ser medido como: quantidade de incidentes
que reabriram ou reincidiram, ou grupos de incidentes de mesma causa. Uma forma é contar
quantos incidentes estão vinculados a problemas (já que isso tipicamente indica recorrência) ou
quantos incidentes após resolvidos voltaram a ocorrer. Também pode ser expresso em
percentual: ex.: “15% dos incidentes do mês se repetiram pelo menos uma vez”. O objetivo é
que, com gestão de problemas efetiva, incidentes recorrentes diminuam. Painéis podem
destacar top 5 tipos de incidentes recorrentes e se há ações de problema em andamento para eles.
Número de Problemas Abertos vs. Encerrados: Um indicador de saúde do gerenciamento de
problemas. Por exemplo, Problemas Encerrados no período (mensal, anual) e Problemas
Novos registrados. Um gráfico pode mostrar acumulo de problemas abertos ao longo do
tempo (backlog de problemas) – se estiver subindo, pode significar que a TI está identificando
muitas causas mas não conseguindo resolvê-las na mesma taxa, ou que o ambiente está
instável. Já problemas encerrados medem a capacidade de eliminar causas raiz efetivamente
. A meta geralmente é encerrar problemas suficiente para reduzir incidentes e manter o
backlog sob controle. O documento do IFTO sugere medir número de problemas relatados e
encerrados anualmente como métricas do processo.
Tempo Médio de Investigação/Resolução de Problemas: Embora o TMRS foque em incidentes,
podemos ter um MTTR de Problemas – o tempo médio para resolver um problema (desde sua
abertura até fechamento definitivo). Isso avalia a velocidade do processo de Problem
Management em encontrar soluções definitivas. É útil especialmente para problemas de alto
impacto.
Taxa de Incidentes vinculados a Problemas: Mede a porcentagem de incidentes que tiveram
uma causa raiz identificada via Problem Management. Um valor alto poderia indicar que muitos
incidentes não são ruídos isolados, mas sintomas de problemas subjacentes – o que, por um
lado, mostra proatividade em identificá-los, mas por outro pode indicar instabilidade nos
serviços. Um valor baixo demais, por outro lado, pode significar que a equipe não está criando
problemas o suficiente (podendo deixar causas raiz passar batido). Monitorar essa taxa ajuda a
equilibrar reativo vs proativo.
SLA de Incidentes – Cumprimento e Violação: Indicador clássico: percentual de incidentes
resolvidos dentro do tempo de SLA acordado. Por exemplo, “% de incidentes críticos resolvidos
em 4h”. O painel deve mostrar a taxa de cumprimento geral e por prioridade. Incidentes fora do
SLA também podem ser listados para análise. A melhora desse indicador ao longo do tempo é
sinal de eficiência e/ou SLAs realistas. Caso haja ANS (Acordo de Nível de Serviço) formal, esse
KPI é reportável.
Backlog de Incidentes Abertos: Número de incidentes abertos pendentes a cada dia/semana,
especialmente os de alta prioridade. Isso dá visão da carga de trabalho e se há acúmulo. Um
gráfico de tendência de backlog (subindo ou descendo) indica se a equipe está conseguindo
atender à demanda.
Distribuição de Incidentes por Categoria/Serviço: Embora não um “indicador” único, um
painel deve mostrar estatísticas de quais tipos de incidentes são mais frequentes (ex.: 30% dos
incidentes do mês foram de categoria “Rede”). Isso ajuda a identificar áreas problemáticas e
priorizar melhorias. Também pode evidenciar necessidade de conhecimento adicional em certa
área (se muitos incidentes repetidos de um tipo ocorrem, talvez falta um artigo de KB ou um
treinamento aos usuários).
Uso da Base de Conhecimento: Indicadores relacionados ao conhecimento, por exemplo:
Número de Artigos criados no período (medindo se o conhecimento está sendo capturado),
## •
## 57
## •
## 62
## 65
## 62
## 6566
## •
## •
## •
## •
## •
## •
## 18

Número de consultas ou visualizações da base (medindo utilização), Taxa de sucesso da base
de conhecimento – esta poderia ser medida via feedback: por ex., se usuários finais usam
portal de conhecimento, quantos resolveram sem abrir chamado (para self-service), ou
internamente, quantos incidentes foram resolvidos usando um artigo (pode ser marcado no
ticket). Um KEDB bem mantido deve refletir em TMRS mais baixo e menos incidentes, então
medir a correlação ou pelo menos a frequência de uso dos artigos de erro conhecido é útil.
Satisfação do Usuário (CSAT) do Suporte: Se o sistema incluir pesquisa pós-atendimento, o
índice de satisfação dos solicitantes é importante. Mesmo que não implementado de início, é
comum ITIL acompanhar se os usuários avaliam bem o suporte (ex.: nota média de 1 a 5). Esse
indicador dá visão qualitativa do serviço.
Tendência de Incidentes (Mês a Mês): Um painel mostrando o volume total de incidentes por
mês ou semana ao longo do ano, possivelmente dividido por severidade. A expectativa é que
conforme problemas definitivos são resolvidos e a TI melhora, o volume de incidentes estabilize
ou diminua. Picos podem indicar eventos anormais ou necessidade de ação (ex.: surto de
incidentes de segurança em certo mês).
Incidentes por Canal de Atendimento: Se relevante, quantos vieram por telefone, e-mail,
portal, etc. Não impacta diretamente ITIL core, mas gerencialmente pode ser interessante (ex.:
se queremos migrar usuários para autoatendimento e base de conhecimento, medir adoção do
portal).
Todos esses indicadores devem ser apresentados em painéis personalizáveis e interativos. Por
exemplo, um gestor poderia clicar no número de problemas abertos para ver a lista deles; ou filtrar o
gráfico de incidentes por categoria. A disponibilidade de informações em tempo real apoia a melhoria
contínua: equipes de TI podem identificar tendências, falhas e oportunidades de correção no processo,
promovendo ações para otimização constante.
Cabe ressaltar que a definição de metas para os indicadores também é importante. No documento do
IFTO, por exemplo, foi definida meta de diminuir o número de problemas abertos e encerrados
anualmente (ou seja, resolver problemas de forma a reduzir tanto a criação quanto resolver os
existentes). Cada organização deve estabelecer suas metas (SLA alvo, % redução de incidentes,
etc.) e o sistema deve suportar configurá-las e sinalizar desvios (por ex., colorir indicador de vermelho
se abaixo da meta).
Em conclusão, a monitoração via KPIs e dashboards é parte integrante do sistema de gestão de
serviços. Incidentes e problemas  devem ser constantemente medidos  para garantir que as
operações de TI estejam eficazes e para  guiar decisões estratégicas  de alocação de recursos e
melhoria de infraestrutura. Uma solução ITSM completa fornece esses insights de forma visual e
acessível, permitindo que dados conduzam as melhorias no processo e, em última instância, elevando
a qualidade dos serviços de TI prestados.
## Referências Utilizadas:
Processo de Gestão de Problemas – IFTO (baseado em ITIL) e trechos correlatos.
Conceitos e boas práticas ITIL em gestão de incidentes e problemas (InvGate, Atlassian, etc.)
## .
Benefícios de integração entre processos e uso de base de conhecimento.
Indicadores de desempenho sugeridos no manual IFTO e literatura (ex: TMRS, problemas
encerrados).
## •
## •
## •
## 59
## 6768
## 6970
## 71
## •
## 15234042
## •
## 30
## 315859
## •
## 411
## •
## 4562
## 19

processo-de-gestao-de-
problemas.pdf
file://file-KsV5LLhWkuF6nY1tQk5UPW
O que é Gerenciamento de Problemas?
https://invgate.com/pt/itsm/problem-management
O que é Gestão de Incidentes?
https://invgate.com/pt/itsm/incident-management
[PDF] processo de gestão de incidentes - IFTO
https://portal.ifto.edu.br/ifto/reitoria/diretoria-sistemica/tecnologia-da-informacao/documentos/processos/processo-de-
gestao-de-incidentes
10 práticas recomendadas para o Gerenciamento eficaz ... - InvGate
https://invgate.com/pt/itsm/problem-management/problem-management-best-practices
Os 11 melhores softwares de ITSM para sua empresa em 2025
https://blog.softexpert.com/pt-br/ferramentas-de-itsm/
## 12345679101415171819202122232425262739404243454647
## 4849505152535455566162636465666768697071
## 813163157
## 111228293032333436374144
## 35
## 38
## 585960
## 20