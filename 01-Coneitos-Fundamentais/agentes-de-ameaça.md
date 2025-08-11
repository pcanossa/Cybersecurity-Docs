# Agentes de Ameaça (Threat Actors)

**Data de Publicação:** 11 de Agosto de 2025  
**Autora:** Patrícia Canossa Gagliardi

## Introdução

Em cibersegurança, não basta saber "como" um ataque acontece; é fundamental entender "quem" o realiza e "por quê". O Agente de Ameaça, ou *Threat Actor*, é a entidade por trás de um incidente de segurança. Compreender seu perfil, suas capacidades e, acima de tudo, suas motivações, é o cerne da disciplina de Inteligência de Ameaças (*Threat Intelligence*). Essa compreensão permite que as organizações passem de uma defesa genérica para uma estratégia de segurança proativa e direcionada, antecipando as ações dos adversários mais prováveis de atacá-las.

---

### 1. O Eixo da Ética: A Classificação por "Chapéus" (Hats)

A primeira camada de classificação, e a mais conhecida, divide os hackers com base na legalidade e ética de suas ações.

* **White Hat (Chapéu Branco):**
    * **Definição:** Um hacker ético que atua estritamente dentro da lei e com autorização explícita. Seu objetivo é encontrar e corrigir falhas de segurança para fortalecer as defesas.
    * **Exemplos de Atuação:** Profissionais de Testes de Penetração (Pentesters), pesquisadores de segurança que participam de programas de *Bug Bounty* (recompensa por falhas), equipes de segurança internas (*Blue Teams*).

* **Black Hat (Chapéu Preto):**
    * **Definição:** Um criminoso que viola a lei para ganho pessoal, para causar danos ou por outras razões maliciosas. Suas ações são ilegais e antiéticas.
    * **Exemplos de Atuação:** Operadores de ransomware, ladrões de dados de cartão de crédito, espiões corporativos. A maioria dos perfis de ameaça se enquadra nesta categoria.

* **Gray Hat (Chapéu Cinza):**
    * **Definição:** Atua em uma zona cinzenta, sem a autorização de um White Hat, mas sem a intenção maliciosa de um Black Hat. Frequentemente, violam a lei para expor uma vulnerabilidade ou provar um ponto.
    * **Exemplos de Atuação:** Um hacker que invade o sistema de uma empresa sem permissão e depois divulga a falha publicamente para forçar a correção.

---

### 2. O Eixo da Motivação e Capacidade: Perfis Detalhados

Esta classificação foca no objetivo final do ator e em seu nível de sofisticação técnica.

#### **Script Kiddies**
* **Perfil:** Atores de baixa habilidade técnica, geralmente inexperientes. O nome deriva de sua dependência de scripts, ferramentas e exploits criados por outros.
* **Motivação:** Vandalismo, curiosidade, busca por reputação em comunidades underground, ou simplesmente o desafio. Geralmente não há ganho financeiro direto.
* **Capacidade e Impacto:** Usam ferramentas prontas para realizar ataques de negação de serviço (DDoS), desfiguração de sites (*defacement*) ou explorar vulnerabilidades bem conhecidas e sem patches. O impacto costuma ser de baixo a moderado.

#### **Hacktivistas**
* **Perfil:** Indivíduos ou grupos que usam o hacking como forma de protesto. A habilidade técnica pode variar drasticamente.
* **Motivação:** Estritamente ideológica. Buscam promover uma agenda política ou social, protestar contra ações de governos ou corporações.
* **Capacidade e Impacto:** Famosos por ataques de DDoS para tirar sites do ar, vazamento de informações confidenciais (*doxing*) para constranger alvos, e *defacement* para disseminar mensagens. O grupo Anonymous é o exemplo mais icônico. O impacto principal é na reputação e na disponibilidade dos serviços.

#### **Corretores de Vulnerabilidades (Vulnerability Brokers)**
* **Perfil:** Pesquisadores de segurança altamente qualificados que descobrem vulnerabilidades e as vendem em um mercado.
* **Motivação:** Principalmente financeira. Operam em uma área eticamente complexa.
* **Capacidade e Impacto:** São especialistas em encontrar falhas complexas, especialmente *zero-days* (vulnerabilidades ainda não conhecidas pelo fabricante). O impacto de seu trabalho depende para quem eles vendem:
    * **Lado "White Hat":** Vender a vulnerabilidade de volta para o fabricante (via Bug Bounty) ou para empresas de segurança.
    * **Lado "Gray Hat":** Vender para agências governamentais ou empresas que desenvolvem ferramentas de vigilância.
    * **Lado "Black Hat":** Vender no mercado negro para cibercriminosos ou APTs.

#### **Cibercriminosos**
* **Perfil:** Profissionais focados em crime digital. Atuam de forma individual ou, mais comumente, em organizações criminosas altamente estruturadas que operam no modelo de *Crime-as-a-Service* (CaaS).
* **Motivação:** Exclusivamente o **lucro financeiro**.
* **Capacidade e Impacto:** Desenvolvem, operam e distribuem malware sofisticado como ransomware, trojans bancários e *infostealers*. São responsáveis por fraudes, roubo de dados em massa e extorsão. O impacto de suas ações é enorme, causando prejuízos de bilhões de dólares anualmente.

#### **Agentes Patrocinados pelo Estado (State-Sponsored / APTs)**
* **Perfil:** A elite do hacking. São unidades de ciberataque financiadas e dirigidas por um governo nacional. São conhecidos como **Advanced Persistent Threats (APTs)** devido à sua natureza furtiva e de longo prazo.
* **Motivação:** Vantagem geopolítica, espionagem industrial e governamental, sabotagem de infraestrutura crítica e vigilância.
* **Capacidade e Impacto:** Possuem os maiores recursos e o mais alto nível técnico. Desenvolvem seus próprios *zero-days*, malwares customizados e conduzem campanhas complexas que podem permanecer ocultas por anos. O impacto é crítico e pode afetar a segurança nacional.

---

### 3. O Contexto Operacional: Da Motivação à Defesa

Entender esses perfis é crucial para a defesa cibernética na prática. A motivação de um ator dita suas táticas:

* Um **Cibercriminoso** usando ransomware precisa ser rápido e barulhento para anunciar a infecção e exigir o pagamento. Suas TTPs (Táticas, Técnicas e Procedimentos) focam em impacto e destruição.
* Uma **APT** em uma missão de espionagem precisa ser lenta, silenciosa e furtiva. Suas TTPs focam em persistência, movimento lateral discreto e exfiltração de dados sem ser detectada.

Ao traçar o perfil do adversário mais provável de atacar seus ativos (um banco se preocupa mais com Cibercriminosos; uma empresa de defesa, com APTs), uma organização pode ajustar seus controles, seu monitoramento e seu plano de resposta a incidentes para detectar e combater os comportamentos específicos daquele tipo de ator.

### Conclusão

O cenário de ameaças é um ecossistema complexo de diferentes atores com objetivos distintos. Classificá-los por sua ética e motivação é o primeiro passo para desmistificar suas ações. Uma estratégia de segurança robusta é aquela que responde à pergunta fundamental: "Quem são nossos adversários e o que eles querem?". Ao responder a essa pergunta, a defesa deixa de ser um escudo genérico e se torna uma barreira inteligente e adaptada ao inimigo real.