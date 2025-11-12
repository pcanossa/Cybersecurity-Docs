# Os 8 Domínios da Cibersegurança 

## Introdução

Para organizar este conhecimento e criar um padrão global para a proficiência em segurança, a (ISC)² desenvolveu o **Common Body of Knowledge (CBK)**, que é estruturado em **8 Domínios de Segurança Cibernética**.

Este framework é a base para a prestigiosa certificação CISSP (Certified Information Systems Security Professional) e funciona como um mapa holístico, cobrindo desde a governança e gestão de riscos até a segurança no desenvolvimento de software. Compreender esses domínios é entender a cibersegurança como uma função estratégica e integrada ao negócio, e não apenas como um problema técnico.

---

### 1. Segurança e Gerenciamento de Riscos (Security and Risk Management)

Este é o domínio fundamental que alinha a estratégia de segurança com os objetivos do negócio. É a "governança" da cibersegurança.
* **Escopo:** Define as políticas, os procedimentos e as estruturas que guiam todo o programa de segurança.
* **Conceitos-Chave:**
    * **Análise de Risco:** Identificar, avaliar e tratar os riscos (como vimos em nosso artigo sobre o tema).
    * **Políticas de Segurança:** Criação de documentos que ditam as regras de segurança da organização.
    * **Conformidade (Compliance):** Garantir que a organização esteja em conformidade com leis e regulamentações (ex: LGPD, PCI-DSS, SOX).
    * **Treinamento e Conscientização:** Educar os funcionários sobre as ameaças e suas responsabilidades.

### 2. Segurança de Ativos (Asset Security)

Este domínio foca na proteção dos ativos mais valiosos da organização: seus dados e informações.
* **Escopo:** Classificação, manuseio e proteção do ciclo de vida dos dados e dos ativos que os armazenam.
* **Conceitos-Chave:**
    * **Classificação da Informação:** Categorizar os dados por nível de sensibilidade (ex: Público, Interno, Confidencial, Restrito).
    * **Propriedade dos Dados:** Definir quem é o responsável por cada conjunto de dados.
    * **Proteção de Dados em Repouso:** Utilizar criptografia para proteger os dados armazenados em discos e bancos de dados.
    * **Gerenciamento do Ciclo de Vida:** Definir como os dados são criados, armazenados, utilizados e, de forma segura, descartados.

### 3. Arquitetura e Engenharia de Segurança (Security Architecture and Engineering)

Este é o domínio do "design e construção". Ele trata de como projetar e implementar sistemas e redes seguras desde o início.
* **Escopo:** Incorporar a segurança na arquitetura de sistemas, redes e aplicações.
* **Conceitos-Chave:**
    * **Modelos de Segurança:** Utilizar frameworks de controle de acesso (ex: Bell-LaPadula).
    * **Criptografia e Criptoanálise:** Entender e aplicar algoritmos criptográficos (simétricos, assimétricos, hashing) e a infraestrutura de chave pública (PKI).
    * **Princípios de Design Seguro:** Aplicar conceitos como Defesa em Profundidade e Negação por Padrão.
    * **Segurança Física:** Proteger data centers e a infraestrutura física contra acesso não autorizado.

### 4. Comunicação e Segurança de Rede (Communication and Network Security)

Este domínio cobre a proteção dos dados em trânsito e da infraestrutura de rede que os transporta. É aqui que se encaixam muitos dos nossos artigos anteriores.
* **Escopo:** Projetar e proteger as redes de comunicação (LAN, WAN, Wi-Fi, etc.).
* **Conceitos-Chave:**
    * **Arquitetura de Rede Segura:** Implementação de firewalls, DMZs e segmentação de rede.
    * **Protocolos de Rede Seguros:** Uso de HTTPS, SSH, VPNs (IPsec/SSL).
    * **Dispositivos de Segurança:** Configuração e gerenciamento de Firewalls, IDS/IPS, Proxies, etc.
    * **Mitigação de Ataques de Rede:** Defesa contra DoS/DDoS, ARP Poisoning, IP Spoofing, etc.

### 5. Gestão de Identidade e Acesso (Identity and Access Management - IAM)

O IAM foca em garantir que as pessoas certas (e apenas as pessoas certas) tenham o acesso correto aos recursos certos.
* **Escopo:** Controle de acesso lógico e físico aos ativos.
* **Conceitos-Chave:**
    * **Framework AAA:** Autenticação, Autorização e Contabilização.
    * **Mecanismos de Autenticação:** Gerenciamento de senhas, biometria, e o mais importante, **Autenticação Multifator (MFA)**.
    * **Controle de Acesso:** Implementação do Princípio do Privilégio Mínimo (PoLP) através de modelos como o RBAC (Role-Based Access Control).
    * **Gerenciamento de Identidades:** Processos para criar, modificar e desativar contas de usuário.

### 6. Avaliação e Testes de Segurança (Security Assessment and Testing)

Este domínio trata de como verificar se os controles de segurança estão implementados corretamente e se são eficazes.
* **Escopo:** Auditoria, teste e monitoramento dos controles de segurança.
* **Conceitos-Chave:**
    * **Teste de Vulnerabilidades (Vulnerability Scanning):** Uso de ferramentas automatizadas para encontrar falhas conhecidas.
    * **Teste de Intrusão (Penetration Testing):** Simulação de um ataque real para testar a resiliência das defesas.
    * **Auditorias de Segurança:** Revisões formais das políticas e configurações.
    * **Análise de Logs e Monitoramento:** Coleta e revisão de logs para detectar atividades anômalas.

### 7. Operações de Segurança (Security Operations)

Este é o domínio do "dia a dia" da cibersegurança, focado na detecção e resposta a incidentes.
* **Escopo:** Atividades operacionais de um Centro de Operações de Segurança (SOC).
* **Conceitos-Chave:**
    * **