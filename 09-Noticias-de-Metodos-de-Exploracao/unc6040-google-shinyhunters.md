# Análise de Incidente: Violação de Dados no Salesforce da Google via Vishing (ShinyHunters/UNC6040)

**Data de Publicação:** 14 de agosto de 2025  
**Nível de Ameaça:** Crítico 
**Autor:** Patrícia Canossa (com base em relatório do Google Cloud)

---

### 1. Resumo Executivo

Em agosto de 2025, a Google confirmou ter sido vítima de uma campanha de violação de dados direcionada a plataformas Salesforce CRM, orquestrada pelo grupo de ameaças `ShinyHunters` (rastreado pelo Google como `UNC6040`). O ataque, que ocorreu em junho, utilizou técnicas de **Vishing** (Phishing por Voz) para manipular funcionários, obter acesso não autorizado a uma das instâncias corporativas do Salesforce da Google e exfiltrar dados de contato de clientes. O incidente faz parte de uma onda de ataques mais ampla que afetou inúmeras grandes corporações, destacando o fator humano como o principal vetor de comprometimento.

### 2. Organização Afetada e Alvo

* **Setor:** Múltiplos, incluindo Tecnologia (Google), Vestuário (Adidas, Louis Vuitton, Dior), Bens de Luxo (Tiffany & Co.), Seguros (Allianz Life) e Aviação (Qantas).  
* **Localização:** Global.  
* **Alvo Principal:** Instâncias de CRM Salesforce. O ponto de entrada são os funcionários, especialmente de equipes de TI e suporte técnico, em divisões de língua inglesa de corporações multinacionais.

O ataque contra a *Google* especificamente comprometeu um sistema *Salesforce* usado para armazenar informações de contato e notas relacionadas a pequenas e médias empresas. Embora a Google tenha afirmado que os dados eram em grande parte públicos, o incidente valida a eficácia das táticas do grupo contra alvos de alto perfil.

### 3. Vulnerabilidade Explorada: Engenharia Social (CWE-300)

* **Identificador:** Não aplicável (N/A) - O ataque não se baseia na exploração de uma vulnerabilidade técnica de software (CVE).  
* **Sistema Afetado:** Processos de suporte de TI e a confiança dos funcionários.  
* **Tipo de Falha (CWE-300):** Violação de Canal ou Caminho (*Channel Accessible by Non-Endpoint*). A manipulação de canais de comunicação legítimos (telefone) para contornar os controles de segurança.  
* **Impacto:** Roubo de credenciais, acesso não autorizado a dados sensíveis de clientes, exfiltração de dados e extorsão financeira.  
* **Status da Correção:** Requer fortalecimento contínuo de processos de verificação de identidade e treinamento de conscientização de segurança.

#### Detalhamento Técnico do Vetor de Ataque

A falha central explorada foi a confiança humana. O grupo `ShinyHunters` não precisou *"hackear"* o *Salesforce*; eles *"hackearam"* as pessoas que o utilizam. A tática consiste em:

1. **Impersonificação Convincente:** Os atacantes se passam por funcionários de TI ou de suporte técnico em chamadas telefônicas.  
2. **Manipulação Psicológica:** Eles criam um senso de urgência ou normalidade para convencer o funcionário-alvo a revelar credenciais de acesso ou a executar ações que contornem a *Autenticação Multifator (MFA)*.  
3. **Acesso Legítimo:** Uma vez com as credenciais, os atacantes obtêm acesso à plataforma Salesforce com as mesmas permissões do usuário comprometido, tornando suas atividades iniciais difíceis de serem detectadas.

### 4. Metodologia do Ataque (Cadeia de Ataque)

O grupo demonstrou uma metodologia evolutiva e sofisticada.

**Fase 1: Reconhecimento e Vishing**

* O atacante identifica funcionários de suporte em empresas-alvo.  
* Ele realiza uma chamada de Vishing, geralmente roteando a conexão através de serviços de *VPN* como `Mullvad` ou `TOR` para ofuscar sua origem.

**Fase 2: Comprometimento de Credenciais e Acesso**

* O funcionário-alvo é convencido a fornecer sua senha ou a aprovar uma notificação de *MFA*.  
* O atacante obtém acesso à rede corporativa e, subsequentemente, à instância do Salesforce.

**Fase 3: Exfiltração de Dados**

* **Evolução Tática:** Inicialmente, o grupo usava ferramentas padrão como o `Salesforce Data Loader`. Em ataques mais recentes, eles passaram a utilizar **scripts Python personalizados** que mimetizam a funcionalidade do Data Loader, tornando a detecção mais difícil.  
* Os scripts automatizam a coleta e o download dos dados do CRM.

**Fase 4: Extorsão**

* Meses após a violação inicial, as vítimas recebem um e-mail de endereços como `shinycorp@tuta.com`, exigindo um resgate em Bitcoin.  
* O grupo dá um prazo curto (normalmente 72 horas) e ameaça vazar ou vender os dados roubados caso o pagamento não seja efetuado. Para aumentar a pressão, eles falsamente alegam ser parte do coletivo ShinyHunters, um nome de grande notoriedade no submundo do crime.

### 5. Análise do Grupo de Ameaça: ShinyHunters (UNC6040)

O `ShinyHunters` é um grupo financeiramente motivado, conhecido por violações de dados em larga escala e subsequente extorsão.

**Principais Características:**

* **Foco em Engenharia Social:** Sua principal arma é o **Vishing**, explorando a confiança em vez de falhas de software.  
* **Possível Sobreposição:** Suas táticas são semelhantes às do grupo `Scattered Spider`, levantando a hipótese de que os grupos compartilham membros ou, no mínimo, *TTPs* (Táticas, Técnicas e Procedimentos).  
* **Falsa Afiliação:** Eles se apropriam do nome `ShinyHunters` para intimidar as vítimas, mesmo que sua identidade real seja rastreada como `UNC6040` pela inteligência de ameaças.  
* **Evolução de Ferramentas:** A mudança de ferramentas padrão para scripts customizados demonstra uma crescente sofisticação técnica e uma tentativa de evadir defesas baseadas em assinaturas.

### 6. Mitigação e Recomendações

1. **Princípio do Menor Privilégio:** Limitar estritamente as permissões de acesso dos usuários, especialmente para ferramentas de exportação de dados em massa como o **Data Loader**.  
2. **Gerenciamento de Aplicações:** Implementar políticas rigorosas de gerenciamento de aplicativos, incluindo **restrições de acesso por IP** e exigência de **MFA** para todas as sessões.  
3. **Detecção de Anomalias:** Utilizar ferramentas como o **Salesforce Shield** para monitorar e alertar sobre atividades suspeitas, como exportações de dados em grande volume ou logins de locais atípicos.  
4. **Treinamento e Conscientização:** Realizar auditorias frequentes e treinamentos contínuos para os funcionários, focando especificamente em como identificar e responder a tentativas de **Vishing** e a ataques de fadiga de **MFA**.  
5. **Verificação Robusta:** Fortalecer os **processos de verificação de identidade** no help desk para solicitações críticas, exigindo múltiplas formas de confirmação antes de redefinir senhas ou credenciais de MFA.