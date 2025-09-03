# Os Cinco Pilares da Segurança da Informação 

**Data de Publicação:** 28 de Agosto de 2025  
**Autora:** Patrícia Canossa Gagliardi

## Introdução

A segurança da informação é uma disciplina que busca proteger os ativos digitais de uma organização ou indivíduo. Para atingir esse objetivo, a prática da segurança da informação se orienta por um conjunto de princípios fundamentais. A compreensão desses princípios é essencial, pois eles definem os objetivos de cada contramedida de segurança. Os cinco pilares mais importantes, frequentemente representados pelos princípios de segurnaça da infomração são: Confidencialidade, Integridade, Disponibilidade, Autenticidade e Não Repúdio, guiam a estratégia para construir um ecossistema digital robusto e resiliente.

---

### 1. Confidencialidade (Confidentiality)

A confidencialidade garante que a informação seja acessada apenas por indivíduos ou sistemas autorizados. É o pilar que protege a privacidade e o sigilo dos dados.

* **Objetivo:** Impedir a divulgação não autorizada de informações sensíveis.
* **Ataques que a violam:**
    * **Roubo de Dados:** Vazamentos de informações de clientes (data breach).
    * **Eavesdropping:** Ataques Man-in-the-Middle que interceptam o tráfego não criptografado.
    * **Acesso Não Autorizado:** Um invasor que consegue acesso a um sistema de arquivos restrito.
* **Contramedidas:**
    * **Criptografia:** O principal controle. Garante que os dados sejam ilegíveis em trânsito (HTTPS) e em repouso (criptografia de disco).
    * **Controle de Acesso:** Impor políticas de acesso mínimo (PoLP) e autenticação forte (MFA) para garantir que apenas os usuários corretos possam acessar os dados.
    * **Firewalls:** Segmentar a rede para isolar zonas com dados sensíveis de outras redes.

---

### 2. Integridade (Integrity)

A integridade assegura que a informação seja exata, completa e não tenha sido alterada de forma não autorizada, seja intencionalmente ou acidentalmente.

* **Objetivo:** Manter a precisão e a confiabilidade dos dados ao longo de todo o seu ciclo de vida.
* **Ataques que a violam:**
    * **Modificação em Trânsito:** Um atacante MitM que altera o conteúdo de uma comunicação.
    * **Injeção de SQL:** Um atacante que consegue modificar registros em um banco de dados.
    * **Vírus:** Um vírus que corrompe arquivos de sistema ou de dados.
* **Contramedidas:**
    * **Assinaturas Digitais e Hashing:** Usar funções hash (como SHA-256) para verificar a integridade de arquivos ou mensagens. Se o hash original e o hash atual não coincidirem, os dados foram alterados.
    * **Protocolos de Integridade:** O TLS/HTTPS não apenas criptografa, mas também garante a integridade dos dados em trânsito.
    * **Validação de Entrada:** Em aplicações web, validar rigorosamente todas as entradas do usuário para prevenir ataques como Injeção de SQL e XSS.

---

### 3. Disponibilidade (Availability)

A disponibilidade garante que os sistemas, aplicações e dados estejam acessíveis e operacionais para os usuários autorizados sempre que necessário.

* **Objetivo:** Assegurar a continuidade do serviço e a resiliência operacional.
* **Ataques que a violam:**
    * **Ataques de Negação de Serviço (DoS/DDoS):** Sobrecarregam um servidor ou uma rede para torná-los indisponíveis.
    * **Ransomware:** Criptografa os dados, tornando-os inacessíveis, a menos que um resgate seja pago.
    * **Worms e Vírus:** Consomem largura de banda ou recursos de processamento, causando lentidão ou falhas.
* **Contramedidas:**
    * **Redundância:** Ter sistemas e serviços duplicados (como servidores de backup ou links de internet redundantes) para garantir que a falha de um não afete o serviço.
    * **Backups:** Manter cópias de segurança confiáveis e fora da rede de todos os dados críticos para permitir a recuperação após um desastre ou ataque de ransomware.
    * **Mitigação de DDoS:** Utilizar serviços especializados em nuvem para absorver ataques volumétricos.

---

### 4. Autenticidade (Authenticity)

A autenticidade garante que a informação ou a origem de uma comunicação seja genuína e verificável.

* **Objetivo:** Provar que a fonte de um dado ou a identidade de um remetente é real.
* **Ataques que a violam:**
    * **Falsificação de E-mail:** Um atacante que se passa por um remetente legítimo em um e-mail de phishing.
    * **IP Spoofing:** Um atacante que falsifica o endereço de origem de um pacote IP para se passar por outro host.
    * **Comprometimento de Certificados Digitais:** A criação de certificados SSL falsos para websites maliciosos.
* **Contramedidas:**
    * **Autenticação Forte:** Uso de MFA (Autenticação Multifator) para verificar a identidade de um usuário.
    * **Autenticação de E-mail:** Implementação de protocolos como **SPF, DKIM e DMARC** para validar a autenticidade dos remetentes de e-mail.
    * **Certificados SSL/TLS:** A infraestrutura de chave pública (PKI) garante que o certificado de um site seja autêntico e confiável.

---

### 5. Não Repúdio (Non-Repudiation)

O não repúdio garante que a origem de uma ação ou transação não possa, posteriormente, negar sua participação. É a prova irrefutável de que a ação foi realizada por aquela entidade.

* **Objetivo:** Fornecer evidências legais e auditáveis de uma ação.
* **Ataques que a violam:** Esta não é uma ameaça no sentido tradicional, mas sim a ausência de um controle de segurança que permite que uma ação maliciosa (ex: um funcionário apagando um arquivo e negando que o fez) seja bem-sucedida.
* **Contramedidas:**
    * **Assinaturas Digitais:** Um documento assinado digitalmente não pode ser negado pela pessoa que o assinou.
    * **Logs de Auditoria:** Logs de acesso e ação (o pilar da Contabilização do AAA) com registros de data e hora imutáveis servem como a principal evidência forense de que uma ação foi realizada por um determinado usuário ou sistema em um momento específico.

### Conclusão

Os cinco pilares da segurança da informação formam a espinha dorsal de qualquer estratégia de defesa. Todas as tecnologias e práticas que exploramos em nossos artigos — firewalls, criptografia, gestão de patches, autenticação multifator, e a análise de logs, são, em última instância, ferramentas para proteger a **confidencialidade, integridade, disponibilidade, autenticidade e não repúdio** dos ativos digitais. Uma postura de segurança madura exige uma abordagem holística que equilibre e fortaleça todos esses pilares, reconhecendo que negligenciar um deles pode comprometer a segurança de toda a organização.