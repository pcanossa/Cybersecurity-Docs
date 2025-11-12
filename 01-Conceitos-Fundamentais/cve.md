# CVE - Common Vulnerabilities and Exposures

## Introdução

No vasto e dinâmico universo da cibersegurança, a clareza e a precisão na comunicação são essenciais. Antes da criação de um padrão, uma mesma falha de segurança podia ser conhecida por diferentes nomes por diferentes fornecedores de software, pesquisadores e ferramentas de segurança, gerando uma enorme confusão.

Para resolver este problema, o **CVE (Common Vulnerabilities and Exposures)** foi criado. Mantido pela MITRE Corporation, o CVE é um dicionário público, de padrão industrial, que fornece um identificador único para cada vulnerabilidade de segurança publicamente conhecida. Ele funciona como o "RG" ou o "CPF" de uma falha, garantindo que todos na comunidade global de segurança estejam falando sobre o mesmo problema de forma inequívoca.

---

### 1. A Anatomia de um Identificador CVE

Cada vulnerabilidade registrada no dicionário recebe um identificador único que segue um formato padronizado e simples:

**`CVE-ANO-NÚMERO`**

* **`CVE`:** O prefixo padrão que identifica o registro.
* **`ANO`:** O ano em que o ID foi atribuído ou a vulnerabilidade foi divulgada publicamente.
* **`NÚMERO`:** Um número sequencial com quatro ou mais dígitos que é atribuído de forma única para cada vulnerabilidade naquele ano.

**Exemplo Prático:** `CVE-2021-44228`
Este identificador refere-se inequivocamente à famosa e crítica vulnerabilidade de execução remota de código na biblioteca Apache Log4j, que foi amplamente divulgada em 2021.

---

### 2. O Ciclo de Vida de um CVE: Do Descobrimento à Publicação

Uma vulnerabilidade não aparece no dicionário CVE magicamente. Ela segue um processo bem definido:

1.  **Descoberta:** Um pesquisador de segurança, um desenvolvedor ou um participante de um programa de "bug bounty" descobre uma nova falha em um software.
2.  **Reporte:** O descobridor reporta a falha de forma responsável a uma **CNA (CVE Numbering Authority)**. As CNAs são mais de 100 organizações globais (como Microsoft, Red Hat, Google, e a própria MITRE) que são autorizadas a atribuir IDs CVE.
3.  **Reserva e Atribuição:** A CNA analisa o reporte. Se a falha for validada como uma nova vulnerabilidade, a CNA **reserva** um ID CVE para ela. Neste ponto, o registro CVE pode ficar em um estado "RESERVADO", sem detalhes públicos, para dar tempo ao fornecedor do software de desenvolver uma correção (patch).
4.  **Divulgação:** Após o fornecedor lançar a correção, os detalhes da vulnerabilidade são tornados públicos. O registro CVE é então preenchido com uma descrição da falha, referências para os avisos de segurança oficiais, e frequentemente, uma pontuação de severidade CVSS.

---

### 3. O Ecossistema de Vulnerabilidades: CVE, CWE e CVSS

É crucial entender como esses três padrões se relacionam. A melhor analogia é com a medicina:

* **CWE (Common Weakness Enumeration):** É o **tipo da doença**. Descreve a fraqueza genérica que tornou a falha possível (ex: `CWE-89: SQL Injection` ou `CWE-79: Cross-Site Scripting`).
* **CVE (Common Vulnerabilities and Exposures):** É o **diagnóstico específico de um paciente**. Descreve a instância única e real daquela doença em um produto específico (ex: `CVE-2023-12345`, uma falha de SQL Injection encontrada no "Software ABC" versão 1.2).
* **CVSS (Common Vulnerability Scoring System):** É a **gravidade do diagnóstico**. É a pontuação de 0.0 a 10.0 que nos diz o quão perigoso é aquele CVE específico para um sistema.

Em resumo: Um desenvolvedor comete um **CWE**, o que resulta em um **CVE** em seu produto, ao qual é atribuída uma pontuação **CVSS**.

---

### 4. Como o CVE é Usado na Prática

O ID CVE é o elo que conecta todo o processo de gerenciamento de vulnerabilidades.

* **Para Profissionais de Segurança e TI:** O CVE é a chave de busca. Quando um fornecedor (como a Microsoft na "Patch Tuesday") lança uma atualização de segurança, o aviso informa: "Esta atualização corrige as vulnerabilidades CVE-2025-XXXXX e CVE-2025-YYYYY". A equipe de segurança usa esses IDs para verificar se seus sistemas estão vulneráveis e priorizar a aplicação do patch.
* **Para Ferramentas de Segurança:** Scanners de vulnerabilidade (como Nessus, Qualys, OpenVAS) têm seus bancos de dados organizados por IDs CVE. A ferramenta varre um sistema, identifica as versões do software em execução e gera um relatório que diz: "Este host está vulnerável ao CVE-2021-44228 porque está executando uma versão vulnerável do Log4j".
* **Para a Comunicação:** O CVE fornece uma linguagem comum. Quando pesquisadores, fornecedores, equipes de TI e a mídia falam sobre o "Log4Shell", todos podem usar o ID `CVE-2021-44228` para garantir que estão se referindo exatamente à mesma falha, eliminando qualquer ambiguidade.

### Conclusão

O sistema CVE é uma inovação simples, mas de impacto profundo, que trouxe ordem e clareza ao mundo caótico do rastreamento de vulnerabilidades. Ao fornecer um identificador único e universal para cada falha de segurança conhecida, o CVE funciona como um pilar para a colaboração. Ele permite que ferramentas automatizadas, processos de gerenciamento de patches e a comunidade global de segurança trabalhem de forma mais rápida, eficiente e coesa para defender os sistemas digitais.