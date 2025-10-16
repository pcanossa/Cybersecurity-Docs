# A Investigação Inicial de um Incidente - O Guia da "Golden Hour"

## Introdução

Um incidente de segurança foi detectado. O alarme soou. Para a equipe de Resposta a Incidentes (CSIRT), começa a "golden hour" — o período inicial e crítico onde a coleta de informações precisas e a estabilização da cena são cruciais. As ações tomadas nesta fase inicial determinam a eficácia de todo o ciclo de vida da resposta a incidentes, desde a contenção até a erradicação.

O objetivo da investigação inicial não é resolver o problema imediatamente, mas sim transformar o caos de um evento desconhecido em um conjunto de dados estruturados. Este guia detalha um fluxo de trabalho metodológico para a coleta de informações essenciais, garantindo que nenhuma evidência volátil seja perdida e que a equipe tenha as informações necessárias para tomar decisões informadas.

---

### Fase 1: A Triagem Inicial - Os 5 Ws do Incidente

O primeiro passo é coletar as informações contextuais básicas, frequentemente chamadas de "os 5 Ws" da investigação (Who, What, When, Where, Why/How).

* **Quando? (When?)**
    * **Data/Hora em que o incidente foi reportado:** Este é o `T0` (tempo zero) da sua linha do tempo de resposta. Use timestamps em UTC para evitar ambiguidades de fuso horário.

* **Quem? (Who?)**
    * **Quem detectou o incidente e/ou quem o reportou?** Obtenha os nomes e contatos. Essas pessoas são as principais testemunhas. Elas podem ter informações contextuais que as ferramentas automáticas não têm.

* **O quê? (What?)**
    * **Qual foi a natureza do incidente?** Classifique-o inicialmente. É um alerta de malware? Uma denúncia de e-mail de phishing? Um sistema que ficou indisponível? Um usuário reportando comportamento estranho em sua máquina?

* **Como? (How?)**
    * **Como o incidente foi detectado?** A detecção foi através de uma ferramenta automatizada (alerta de EDR, IPS, SIEM) ou por um usuário final? Isso ajuda a entender a eficácia dos seus controles de segurança.

* **Onde? (Where?)**
    * **Quais são os sistemas impactados?** Inicie uma lista de todos os sistemas (hostnames, IPs) que foram reportados ou que estão diretamente associados ao alerta.

---

### Fase 2: Escopo e Perfilamento dos Ativos Impactados

Com a triagem inicial feita, o próximo passo é entender a "cena do crime" digital. Para cada sistema impactado identificado na Fase 1, colete um perfil detalhado.

* **Identificação do Ativo:**
    * **Hostnames e Endereços IP:** Essencial para correlação em logs de rede.
    * **Sistema Operacional:** Incluindo a versão e o nível de patch. Isso é crucial para pesquisar vulnerabilidades potenciais.
    * **Localização Física:** Onde o servidor ou a estação de trabalho está fisicamente localizada?

* **Contexto de Negócio:**
    * **Propósito do Sistema:** É um servidor web de produção? Um banco de dados de clientes? Uma estação de trabalho de um desenvolvedor? Isso determina a criticidade e o impacto potencial do incidente.
    * **Proprietário do Sistema (System Owner):** Quem é o responsável de negócio por este ativo?

* **Estado Atual do Sistema:**
    * O sistema está online, offline, ou foi isolado da rede?
    * **Crucial:** O sistema foi reiniciado? Uma reinicialização destrói toda a evidência volátil da memória RAM.

---

### Fase 3: Crônica de Ações e Situação Atual

É vital manter um registro de todas as ações tomadas desde a detecção do incidente. Este é o início da sua **Cadeia de Custódia**.

* **Crie um Log de Analista:** Mantenha um registro com timestamp de cada ação.
    * **Quem acessou os sistemas impactados?** Registre o nome de cada administrador ou analista.
    * **Quais ações foram tomadas?** O usuário tentou rodar um antivírus? O administrador tentou reiniciar o serviço? Essas ações, mesmo que bem-intencionadas, alteram o estado do sistema e precisam ser documentadas.

* **Avaliação do Estado do Incidente:**
    * **É um incidente em andamento?** A atividade suspeita ainda está ocorrendo, ou ela já parou? Isso determina a urgência da fase de contenção.

---

### Fase 4: Preservação de Evidências (Se Malware Estiver Envolvido)

Se houver suspeita de malware, a preservação de evidências se torna a prioridade máxima, seguindo a **Ordem da Volatilidade**.

* **Coleta de Evidências Voláteis (se o sistema estiver ligado):**
    * Conexões de rede ativas.
    * Processos em execução.
    * Contas logadas.
    * **Dump de Memória RAM:** A evidência mais rica.

* **Coleta de Evidências Persistentes:**
    * **Isolamento do Artefato Malicioso:** Exporte os arquivos maliciosos suspeitos para um ambiente de análise seguro.
    * **Criação da "Impressão Digital" (Hashing):** Para cada arquivo exportado, calcule seu hash criptográfico (SHA256, MD5). Isso cria um identificador único e garante a integridade da evidência.
        * `SHA256: f25a780095730701efac67e9d5b84bc289afea56d96d8aff8a44af69ae606404`
    * **Documentação Forense:** Mantenha um registro associando o hash a uma cópia segura do arquivo, juntamente com o timestamp e a origem da detecção.
    * **Imagem de Disco:** Em casos graves, a criação de uma imagem forense completa do disco do sistema pode ser necessária para uma análise mais profunda.

---

### Exemplo de Relatório de Coleta Inicial

| Campo | Informação Coletada |
| :--- | :--- |
| **ID do Incidente** | INC-20251016-001 |
| **Data/Hora da Detecção**| 2025-10-16 13:45:00 UTC |
| **Detectado Por** | Alerta de EDR (CrowdStrike) |
| **Reportado Por** | SOC Nível 1 (automatizado) |
| **Tipo de Incidente** | Malware (Potencial Ransomware) |
| **Sistemas Impactados** | `SRV-FIN-01` (10.10.20.5), `WKSTN-JSMITH` (10.10.30.12) |
| **Estado do Incidente** | Em andamento (processo suspeito ainda ativo em SRV-FIN-01). |
| **Ações Tomadas** | `13:50 UTC`: Analista (J.Silva) isolou SRV-FIN-01 da rede via EDR. |
| **Evidência Coletada** | `malicious.exe` (SHA256: `abc...def`), Dump de memória de SRV-FIN-01. |

---

### Conclusão

A investigação inicial de um incidente é um processo metodológico que visa estabelecer o controle da situação e preservar as evidências. Ao seguir um fluxo de trabalho estruturado para coletar informações sobre o evento, os ativos impactados, as ações já tomadas e as evidências digitais, a equipe de resposta a incidentes constrói a fundação sólida necessária para as próximas fases do ciclo de vida da resposta: Contenção, Erradicação e Recuperação. Uma coleta inicial bem executada é o que possibilita uma análise precisa e uma resolução bem-sucedida do incidente.