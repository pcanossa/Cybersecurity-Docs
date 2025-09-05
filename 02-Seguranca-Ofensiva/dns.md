# Registros DNS - A Anatomia da Resolução de Nomes

**Data de Publicação:** 5 de Setembro de 2025  
**Autora:** Patrícia Canossa Gagliardi

## Introdução

O Sistema de Nomes de Domínio (DNS) é frequentemente descrito como a "lista telefônica da internet", mas essa analogia subestima sua complexidade e poder. Na realidade, o DNS é um banco de dados hierárquico e distribuído globalmente. As informações contidas neste banco de dados são organizadas em unidades chamadas **Registros de Recursos (RR - Resource Records)**. Cada registro é como um pequeno "documento" que fornece uma informação específica sobre um domínio.

Entender os diferentes tipos de registros e saber como consultá-los é uma habilidade fundamental para qualquer profissional de TI e cibersegurança, pois eles revelam a arquitetura de uma rede, o fluxo de e-mails e, crucialmente, as políticas de segurança de um domínio.

---

### 1. Como Acessar/Consultar Registros DNS

Para "ler" esses registros, utilizamos ferramentas de linha de comando que consultam os servidores DNS. As duas mais comuns são `nslookup` e `dig`.

* **`nslookup` (Name Server Lookup):**
    * Uma ferramenta presente na maioria dos sistemas operacionais, incluindo o Windows. É simples e direta para consultas rápidas.
    * **Uso:** `nslookup [opções] [nome_do_dominio]`
    * **Exemplo:** Para encontrar o endereço IP (Registro A) de `google.com`:
        ```bash
        nslookup google.com
        ```

* **`dig` (Domain Information Groper):**
    * A ferramenta padrão em ambientes Linux e macOS, preferida por profissionais por fornecer uma saída muito mais detalhada e estruturada.
    * **Uso:** `dig [nome_do_dominio] [tipo_de_registro]`
    * **Exemplo:** Para consultar especificamente os servidores de e-mail (Registro MX) do `google.com`:
        ```bash
        dig google.com MX
        ```

---

### 2. Os Principais Tipos de Registros DNS

Existem dezenas de tipos de registros, mas um punhado deles forma a base da maioria das operações na internet.

* **`A` (Address Record):**
    * O registro mais fundamental. Mapeia um nome de domínio para um **endereço IPv4** (ex: `172.217.29.14`).

* **`AAAA` (IPv6 Address Record):**
    * O equivalente do registro A, mas para o **endereço IPv6**.

* **`CNAME` (Canonical Name Record):**
    * Funciona como um "apelido" (alias). Ele mapeia um nome de domínio para outro nome de domínio. Por exemplo, `ftp.empresa.com` pode ser um `CNAME` para `arquivos.provedor.com`.

* **`MX` (Mail Exchanger Record):**
    * Especifica quais servidores são responsáveis por receber os **e-mails** de um domínio. Cada registro MX tem um número de prioridade que indica a ordem de preferência (quanto menor o número, maior a prioridade).

* **`NS` (Name Server Record):**
    * Delega a autoridade sobre um domínio, especificando quais são os **servidores de nomes autoritativos** para aquela zona.

---

### 3. O Registro `TXT`: O Canivete Suíço do DNS

O registro `TXT` foi originalmente criado para conter texto informativo arbitrário sobre um domínio. No entanto, sua natureza flexível o transformou em uma das ferramentas mais importantes para a **segurança e verificação de serviços** na internet moderna.

Enquanto outros registros têm um formato rígido, um registro `TXT` pode conter praticamente qualquer string de texto, permitindo que os administradores publiquem informações para serem lidas por outros sistemas automatizados.

#### **Aplicações de Segurança Críticas do Registro `TXT`:**

* **SPF (Sender Policy Framework):**
    * O SPF é um mecanismo de autenticação que combate a falsificação de e-mails. A política SPF de um domínio é publicada em um registro `TXT`.
    * **Exemplo de consulta:** `dig google.com TXT`
    * **Resultado (pode incluir):** `"v=spf1 include:_spf.google.com ~all"`
    * Esta linha, dentro de um registro `TXT`, informa aos servidores de e-mail do mundo quais endereços IP estão autorizados a enviar e-mails em nome de `google.com`.

* **DKIM (DomainKeys Identified Mail):**
    * Outro padrão de autenticação de e-mail que usa uma assinatura digital. A **chave pública** necessária para verificar essa assinatura é publicada dentro de um registro `TXT` em um subdomínio específico.
    * **Exemplo de consulta:** `dig 20230601._domainkey.google.com TXT`

* **DMARC (Domain-based Message Authentication, Reporting, and Conformance):**
    * A política que une o SPF e o DKIM também é publicada como um registro `TXT` em um subdomínio específico (`_dmarc.dominio.com`).
    * **Exemplo de consulta:** `dig _dmarc.google.com TXT`
    * **Resultado (pode incluir):** `"v=DMARC1; p=reject; rua=mailto:mailauth-reports@google.com"`

* **Verificação de Propriedade de Domínio:**
    * Muitos serviços online (Google, Microsoft 365, etc.) precisam confirmar que você é o verdadeiro dono de um domínio antes de permitir que você o utilize. O método mais comum é pedir que você crie um registro `TXT` com um código de verificação único. O serviço então consulta o registro `TXT` do seu domínio; se encontrar o código, a propriedade é confirmada.

### Conclusão

O DNS é muito mais do que um simples sistema de tradução de nomes para IPs. Ele é uma base de dados complexa, cujos "documentos" — os Registros de Recursos — definem a arquitetura e as políticas de segurança de um domínio. Para um analista de cibersegurança, a capacidade de consultar e interpretar estes registros, especialmente o versátil registro `TXT`, é uma habilidade indispensável. É através da análise desses registros que se pode investigar campanhas de phishing, verificar a configuração de segurança de um parceiro ou realizar o reconhecimento inicial em um teste de intrusão.