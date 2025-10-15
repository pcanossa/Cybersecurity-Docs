# Desmembrando o Core do NIST CSF - Funções, Categorias e Exemplos

## Introdução

O Núcleo (Core) do NIST Cybersecurity Framework é o coração da estrutura, fornecendo o "o que" de um programa de cibersegurança. Ele apresenta um conjunto de atividades e resultados de segurança desejáveis, organizados de forma lógica e hierárquica, que são comuns a diversos setores e organizações.

A estrutura do Core é projetada para ser intuitiva, dividida em três níveis de detalhe: **Funções**, **Categorias** e **Subcategorias**. Compreender essa hierarquia é o primeiro passo para utilizar o framework para avaliar e aprimorar a postura de segurança de uma organização. Este artigo detalha as Categorias dentro de cada uma das cinco Funções do Core e fornece exemplos práticos de Subcategorias.

---

### 1. Função: IDENTIFICAR (Identify - ID)

**Objetivo:** Desenvolver a compreensão organizacional para gerenciar o risco de cibersegurança para sistemas, ativos, dados e capacidades. Esta função é a base de todo o programa de segurança; sem entender o que se precisa proteger, é impossível fazê-lo de forma eficaz.

#### **Categorias da Função IDENTIFICAR:**

* **Gestão de Ativos (ID.AM):** Foca em inventariar e gerenciar todos os ativos de TI (físicos e lógicos) e de dados para que a organização saiba o que precisa proteger.
    * **Exemplo de Subcategoria:** `ID.AM-2`: Plataformas de software e aplicações dentro da organização são inventariadas.

* **Ambiente de Negócio (ID.BE):** Trata de compreender a missão da organização, seus objetivos e seu lugar na cadeia de suprimentos, para que as decisões de segurança possam apoiar as prioridades estratégicas do negócio.
    * **Exemplo de Subcategoria:** `ID.BE-1`: A missão e os objetivos da organização são compreendidos e comunicados.

* **Governança (ID.GV):** Envolve o estabelecimento de políticas, procedimentos e processos para gerenciar e monitorar os requisitos regulatórios, legais, de risco e operacionais da organização.
    * **Exemplo de Subcategoria:** `ID.GV-1`: Uma política de segurança da informação organizacional foi estabelecida.

* **Avaliação de Risco (ID.RA):** O processo de identificar, analisar e avaliar os riscos de cibersegurança para a organização.
    * **Exemplo de Subcategoria:** `ID.RA-1`: Vulnerabilidades em ativos são identificadas e documentadas.

* **Estratégia de Gestão de Risco (ID.RM):** Trata de estabelecer o apetite e a tolerância a riscos da organização e de desenvolver uma estratégia para lidar com os riscos identificados.
    * **Exemplo de Subcategoria:** `ID.RM-1`: Os processos de gestão de risco são estabelecidos, gerenciados e acordados pelas partes interessadas da organização.

* **Gestão de Risco da Cadeia de Suprimentos (ID.SC):** Foca em identificar e gerenciar os riscos associados a fornecedores e parceiros externos.
    * **Exemplo de Subcategoria:** `ID.SC-1`: Processos de gestão de risco da cadeia de suprimentos são identificados, estabelecidos e acordados.

---

### 2. Função: PROTEGER (Protect - PR)

**Objetivo:** Desenvolver e implementar as salvaguardas e controles de segurança apropriados para garantir a entrega de serviços críticos. Esta função apoia a capacidade de limitar ou conter o impacto de um evento de cibersegurança.

#### **Categorias da Função PROTEGER:**

* **Gestão de Identidade e Controle de Acesso (PR.AC):** Garante que apenas usuários, processos e dispositivos autorizados tenham acesso aos ativos, com base no princípio do privilégio mínimo.
    * **Exemplo de Subcategoria:** `PR.AC-4`: O acesso a ativos e instalações associadas é gerenciado, incorporando o princípio do privilégio mínimo.

* **Conscientização e Treinamento (PR.AT):** Trata de educar e treinar funcionários e parceiros para que eles compreendam suas responsabilidades de segurança.
    * **Exemplo de Subcategoria:** `PR.AT-1`: Todos os usuários são informados e treinados.

* **Segurança de Dados (PR.DS):** Foca na proteção da confidencialidade, integridade e disponibilidade dos dados, em repouso, em trânsito e em uso.
    * **Exemplo de Subcategoria:** `PR.DS-1`: Dados em repouso são protegidos.
    * **Exemplo de Subcategoria:** `PR.DS-2`: Dados em trânsito são protegidos.

* **Processos e Procedimentos de Proteção da Informação (PR.IP):** Envolve o estabelecimento de políticas e procedimentos para o gerenciamento do ciclo de vida seguro dos sistemas.
    * **Exemplo de Subcategoria:** `PR.IP-1`: Uma linha de base de configurações seguras é criada, mantida e usada.

* **Manutenção (PR.MA):** Trata da manutenção e reparo de componentes do sistema de informação de forma consistente com as políticas e procedimentos.
    * **Exemplo de Subcategoria:** `PR.MA-1`: Ferramentas de manutenção e reparo são gerenciadas.

* **Tecnologia de Proteção (PR.PT):** Envolve a implementação de soluções técnicas de segurança, como logs, controles de integridade e redes resilientes.
    * **Exemplo de Subcategoria:** `PR.PT-1`: Registros de auditoria/log são determinados, documentados, implementados e revisados.

---

### 3. Função: DETECTAR (Detect - DE)

**Objetivo:** Desenvolver e implementar as atividades apropriadas para identificar a ocorrência de um evento de cibersegurança de forma oportuna.

#### **Categorias da Função DETECTAR:**

* **Anomalias e Eventos (DE.AE):** Garante que atividades anômalas sejam detectadas e que o impacto potencial dos eventos seja compreendido.
    * **Exemplo de Subcategoria:** `DE.AE-1`: Uma linha de base de operações de rede e fluxo de dados esperado é estabelecida.

* **Monitoramento Contínuo da Segurança (DE.CM):** Envolve o monitoramento contínuo dos sistemas e da rede para identificar eventos de cibersegurança e verificar a eficácia dos controles de proteção.
    * **Exemplo de Subcategoria:** `DE.CM-1`: A rede física e os sistemas são monitorados para detectar eventos de cibersegurança.

* **Processos de Detecção (DE.DP):** Trata de manter e testar os processos e procedimentos de detecção para garantir a prontidão e a conscientização.
    * **Exemplo de Subcategoria:** `DE.DP-4`: Os logs de eventos são agregados e correlacionados de múltiplas fontes.

---

### 4. Função: RESPONDER (Respond - RS)

**Objetivo:** Desenvolver e implementar as atividades apropriadas a serem tomadas após a detecção de um incidente, apoiando a capacidade de conter seu impacto.

#### **Categorias da Função RESPONDER:**

* **Planejamento da Resposta (RS.RP):** Garante que os processos e procedimentos de resposta sejam executados e mantidos.
    * **Exemplo de Subcategoria:** `RS.RP-1`: O plano de resposta a incidentes é executado durante ou após um evento.

* **Comunicações (RS.CO):** Garante que as atividades de resposta sejam coordenadas com as partes interessadas internas e externas.
    * **Exemplo de Subcategoria:** `RS.CO-2`: As informações são compartilhadas de acordo com o plano de resposta.

* **Análise (RS.AN):** Conduz a análise para garantir uma resposta eficaz e apoiar a recuperação.
    * **Exemplo de Subcategoria:** `RS.AN-1`: As notificações de fontes de detecção são investigadas.

* **Mitigação (RS.MI):** Envolve as atividades para prevenir a expansão de um evento e mitigar seus efeitos.
    * **Exemplo de Subcategoria:** `RS.MI-1`: Os incidentes são contidos.

* **Melhorias (RS.IM):** Trata de incorporar as "lições aprendidas" para aprimorar as atividades de resposta.
    * **Exemplo de Subcategoria:** `RS.IM-1`: As atividades de resposta a incidentes são aprimoradas incorporando as lições aprendidas.

---

### 5. Função: RECUPERAR (Recover - RC)

**Objetivo:** Desenvolver e implementar as atividades apropriadas para manter planos de resiliência e restaurar quaisquer capacidades ou serviços que foram prejudicados.

#### **Categorias da Função RECUPERAR:**

* **Planejamento da Recuperação (RC.RP):** Garante que os processos e procedimentos de recuperação sejam executados e mantidos.
    * **Exemplo de Subcategoria:** `RC.RP-1`: O plano de recuperação é executado durante ou após um evento.

* **Melhorias (RC.IM):** Trata de incorporar as "lições aprendidas" para aprimorar as estratégias de recuperação.
    * **Exemplo de Subcategoria:** `RC.IM-2`: As estratégias de recuperação são atualizadas.

* **Comunicações (RC.CO):** Garante que as atividades de recuperação sejam coordenadas com as partes interessadas.
    * **Exemplo de Subcategoria:** `RC.CO-1`: As relações públicas são gerenciadas.

### Conclusão

O Núcleo do NIST CSF fornece um vocabulário abrangente e uma estrutura lógica para o gerenciamento do risco de cibersegurança. Ao desmembrar o complexo campo da segurança nas cinco funções de Identificar, Proteger, Detectar, Responder e Recuperar, e detalhar cada uma delas em Categorias e Subcategorias acionáveis, o framework oferece um caminho claro para que as organizações avaliem sua postura atual, definam seus objetivos e construam um programa de segurança mais maduro e resiliente.